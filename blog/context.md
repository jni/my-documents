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

# Over-representation analysis tutorial

# Gene set enrichment analysis

# Pathway analysis
