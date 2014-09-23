Interpreting (ranked) lists of genes
====================================

Many genomic studies output lists of genes in one form or another. For example,
gene expression studies produce genes that are up- or down-regulated in one
condition relative to another; genome-wide association studies return genomic
regions that are preferentially associated with a particular disease or
condition; and DNA methylation measurements result in lists of differentially
methylated gene promoters.

How can we draw meaningful conclusions from such lists? There's a few
options...

1. Scan the list for a gene you recognise, shout "eureka!", and construct an
   elaborate story about that gene's role in your experiment.
2. Try to place the genes in context: using previously known relationships
   between the genes in your list, determine which sets of genes are working in
   concert. *Then*, cherry pick from the list of contexts to construct an
   elaborate story about that context's role in your study. (See [here]
   (http://liorpachter.wordpress.com/2014/02/12/why-i-read-the-network-nonsense-papers/)
   under "The nature of man" for an example of this approach.)
3. Place the genes in context (as above) and use a systematic approach to
   choose which contexts to interpret.

There will be no medals awarded for correctly guessing which approach we will
pursue in this tutorial.

# Categorisation of context-generating methods

In 2012, Khatri *et al*. published a
[review](http://www.ploscompbiol.org/article/info%3Adoi%2F10.1371%2Fjournal.pcbi.1002375)
in PLoS Comp. Biol. of various methods for determining gene context for gene
lists. (They refer to it as "pathway analysis", but that is a very overloaded
term, which I prefer to reserve for methods that use gene network information
of various types.) I'm not a huge fan of the review in general, because it
fails to prescribe any one method. Instead, the authors content themselves with
a simple enumeration of some of the more popular methods/tools, attaching a
brief description of each.

Having said that, they did very neatly categorise the various options
available, and I think their method classes are intuitive, well justified, and
useful. So, I proceed to parrot them below, along with my favourite tool and
software choices for each.

# Over-representation analysis

## Introduction

This is the oldest, most common, most easily interpretable, and most
well-developed of the bunch. As such, it is certainly the approach I recommend
as a first stop. Though, as we will see, there are plenty of common pitfalls to
avoid, and the results are not always any more interpretable than your original
list of genes.

Suppose we perform a simple experiment, say, compare the expression level of
every gene in a set of tumour samples or a set of non-tumour samples. And say
that we have such clean data that *exactly* 947 genes have higher expression in
tumour samples than normal ones. (They are all wildly statistically
significant, and all others are very much non-significant.)

Suppose further that we can categorise genes in the human genome into exactly
two categories: "kinase" and "non-kinase". And that exactly 947 genes (out of
thousands) are kinases. *And*, those 947 genes are exactly the 947 that are
overexpressed in our tumour samples. Well, we would have a pretty strong hunch
that kinases have something to do with tumours!

But what if our overexpressed genes only contained 946 kinases? What about 522?
Or 95? At which point do we decide that it's not an interesting number of
kinases in our overexpressed gene list?

And what if there's more than one interesting category of genes? What if, in
addition to kinases, there's DNA binding proteins, methylases, and
phosphatases?

Over-representation analysis (ORA) provides the answer to these questions.

## The hypergeometric test

The formal test of the above example is formulated as follows: given that there
are $n$ genes labelled X out of $N$ genes total, and we have drawn $m$ genes
at random from the set of all genes, what is the probability that $k$ or more
of the drawn genes are labelled with category X? The answer is provided by the
[hypergeometric
distribution](http://mathworld.wolfram.com/HypergeometricDistribution.html).
(See [this link](http://www.math.uah.edu/stat/urn/Hypergeometric.html) for
helpful exercises relating to this distribution.)
(See also John Cook's [awesome
chart](http://www.johndcook.com/distribution_chart.html) detailing the
relationship between various distributions.)

\\[
\begin{align}
\Pr(X = k) & = & \frac{{m \choose k} {N - m \choose n - k}} {{N \choose n}} \\

\Pr(X \geq k) & = & \textstyle \sum_{i=k}^{\min(n, m)}{\Pr(X = k)}
\end{align}
\\]

The idea is that if the second probability is small, then we can conclude that
our initial model (that we chose the genes at random, with regards to this
label X) is false. (This is a *frequentist approach* and not exactly correct!
But, we will deal with that later in this document.)

## Using the test

To use this overrepresentation analysis, we need a source of annotations:
labels for the genes. A common source is the [Gene
Ontology](http://www.geneontology.org/). This has a set of *hierarchical*,
*overlapping* annotations of most genes in the genome. Let's break that down:

- hierarchical: a gene that codes for a *promoter-region binding protein* also
  codes for a *DNA binding protein*. All promoter-region binding proteins are
  also DNA binding proteins.
- overlapping: a protein can be both DNA binding *and* have kinase activity.

Other sources include [OMIM](http://www.omim.org/) and
[GeneRIF](http://www.ncbi.nlm.nih.gov/gene/about-generif), but we will focus on
GO because it is the most commonly used.

We also need some genes! If you have your own list of genes, feel free to use
it, but for the rest of us, we will select a subset from an arbitrary gene
expression experiment, namely, that of Lappalainen *et al*, 2013. (This article
is freely available on PubMed Central
[here](http://www.ncbi.nlm.nih.gov/pmc/articles/PMC3918453/).

You can download the feature counts (that is, how many reads were observed for
each gene) [here](). We have looked for genes that are differentially expressed
between males and females using [this Python gist](), obtaining, finally, a
list of genes having a False Discovery Rate (FDR) lower than 0.01, found
[here](). Additionally, we can separate these into up- and down-regulated
genes ([here]() and [here]()). Now, we want to know which functional categories
in GO are overrepresented in these lists.

One important thing to note about testing these three different lists: many
biological function annotations are direction-insensitive. For example, genes
could be annotated as being involved in "cell cycle progression" whether they
are promoters of inhibitors of such a function. Therefore, it makes sense to
treat "significantly differentially expressed" genes, regardless of direction
of change, as a coherent subset.

Download the gene lists linked above, then go to the
[GOrilla homepage]().
Paste your list of genes into the XXX box. For the background list box, include
the full list of genes ([here]()).
This is from the gene model file used to obtain read counts.

GOrilla will return an image of the GO hierarchy, with the overrepresented
categories highlighted in yellow, orange, and red (increasing levels of
significance):

![GOrilla output]()

From this point it is up to you to interpret the gene functions
that come up as significant here! Automatic synthesis is an area of ongoing
research, but not quite ready for primetime.

Finally, note that GOrilla is just one tool for overrepresentation analysis.
Here is a list of alternatives. They fundamentally do much of the same thing,
but their interface (web-based, R, Python, etc.) might better suit your own
purposes.

* DAVID
* GOstat
* GOSeq

# Gene set enrichment analysis

# Pathway analysis


