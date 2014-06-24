
This year I am privileged to be a mentor in the
[Google Summer of Code](https://www.google-melange.com/gsoc/homepage/google/gsoc2014)
for the [scikit-image](http://scikit-image.org) project, as part of the Python
Software Foundation organisation. Our student,
[Vighnesh Birodkar](https://github.com/vighneshbirodkar), recently came up with
a clever use of SciPy's
[`ndimage.generic_filter`](http://docs.scipy.org/doc/scipy/reference/generated/scipy.ndimage.filters.generic_filter.html)
that is certainly worth sharing widely.

Vighnesh is
[tasked](http://www.google-melange.com/gsoc/proposal/public/google/gsoc2014/vighneshbirodkar/5870670537818112)
with implementing region adjacency graphs and graph based methods for image
segmentation. He initially wrote specific functions for 2D and 3D images, and I
suggested that he should merge them: either with n-dimensional code, or, at the
very least, by making 2D a special case of 3D. He chose the former, and produced
extremely elegant code. Three nested for loops and a large number
of neighbour computations were replaced by a function call and a simple loop.
Read on to find out how.

Iterating over an array of unknown dimension is not trivial a priori, but
thankfully, someone else has already solved that problem: NumPy's
[`nditer`](http://docs.scipy.org/doc/numpy/reference/generated/numpy.nditer.html)
and
[`ndindex`](http://docs.scipy.org/doc/numpy/reference/generated/numpy.ndindex.html)
functions allow one to efficiently iterate through every point of an
n-dimensional array. However, that still leaves the problem of finding
neighbors, to determine which regions are adjacent to each other. Again, this
is not trivial to do in nD.

scipy.ndimage provides a suitable function, `generic_filter`. Typically, a
filter is used to iterate a "selector" (called a structuring element) over an
array, compute some function of all the values covered by the structuring
element, and replace the central value by the output of the function. For
example, using the structuring element:

```
fp = np.array([[0, 1, 0],
               [1, 1, 1],
               [0, 1, 0]], np.uint8)
```

and the function `np.median` on a 2D image produces a median filter over a
pixel's immediate neighbors. That is,

```python
import functools
median_filter = functools.partial(generic_filter,
                                  function=np.median,
                                  footprint=fp)
```

Here, we don't want to create an output array, but an output graph. What to do?
As it turns out, Python's pass-by-reference allowed Vighnesh to do this quite
easily using the "extra_arguments" keyword to `generic_filter`: we can write a
filter function that receives the graph and updates it when two distinct values
are adjacent! `generic_filter` passes all values covered by a structuring
element as a flat array, in the array order of the structuring element. So
Vighnesh wrote the following function:

```python
def _add_edge_filter(values, g):
    """Add an edge between first element in `values` and
    all other elements of `values` in the graph `g`.
    `values[0]` is expected to be the central value of
    the footprint used.

    Parameters
    ----------
    values : array
        The array to process.
    g : RAG
        The graph to add edges in.

    Returns
    -------
    0.0 : float
        Always returns 0.

    """
    values = values.astype(int)
    current = values[0]
    for value in values[1:]:
        g.add_edge(current, value)
    return 0.0
```

Then, using the footprint:

```python
fp = np.array([[0, 0, 0],
               [0, 1, 1],
               [0, 1, 0]], np.uint8)
```

(or its n-dimensional analog), this filter is called as follows on `labels`, the
image containing the region labels:

```python
filters.generic_filter(labels,
                       function=_add_edge_filter,
                       footprint=fp,
                       mode='nearest',
                       extra_arguments=(g,))
```

This is a rather unconventional use of generic_filter, which is normally used
for its output array. Note how the return value of the filter function,
`_add_edge_filter`, is just 0! In our case, the output array contains all
0s, but we use the filter _exclusively for its side-effect_: adding an edge to
the graph g when there is more than one unique value in the footprint. That's
cool.

Continuing, in this first RAG implementation, Vighnesh wanted to segment
according to
average color, so he further needed to iterate over each pixel/voxel/hypervoxel
and keep a running total of the color and the pixel count. He used elements in
the graph node dictionary for this and updated them using `ndindex`:

```python
for index in np.ndindex(labels.shape):
    current = labels[index]
    g.node[current]['pixel count'] += 1
    g.node[current]['total color'] += image[index]
```

Thus, together, numpy's `nditer`, `ndindex`, and scipy.ndimage's
`generic_filter` provide a powerful way to perform a large variety of operations
on n-dimensional arrays... Much larger than I'd realised!

You can see Vighnesh's complete pull request
[here](https://github.com/scikit-image/scikit-image/pull/1031) and follow his
blog [here](http://vcansimplify.wordpress.com/).
