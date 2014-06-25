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

In 2012, Khatri _et al_. published a [review](
http://www.ploscompbiol.org/article/info%3Adoi%2F10.1371%2Fjournal.pcbi.1002375)
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
that we have such clean data that _exactly_ 947 genes have higher expression in
tumour samples than normal ones. (They are all wildly statistically
significant, and all others are very much non-significant.)

Suppose further that we can categorise genes in the human genome into exactly
two categories: "kinase" and "non-kinase". And that exactly 947 genes (out of
thousands) are kinases. _And_, those 947 genes are exactly the 947 that are
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



# Gene set enrichment analysis

# Pathway analysis
