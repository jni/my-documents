Book Proposal
=============

Proposed Book Title: **Elegant SciPy**

Proposed Book Subtitle: **Learn Scientific Python from the best code on the internet.**

Author(s): **Juan Nunez-Iglesias**,
**Stéfan van der Walt**,
**Harriet Dashnow**

Author title(s) and affiliation(s):

**JNI: Research Scientist, Victorian Life Science Computation Initiative, University of Melbourne**

**SJVDW: Stellenbosch University / UC Berkeley**

**HD: Bioinformatician, Life Sciences Computation Centre, University of Melbourne**

Preferred mailing address(es):

<b>Juan Nunez-Iglesias  
VLSCI  
187 Grattan Street  
Carlton, VIC, 3010</b>

Preferred phone number: +61 416 155574

Preferred Email address(es): jni.soma@gmail.com

## Author Platform details:

### Author biography and LinkedIn profile: 

https://www.linkedin.com/in/jnuneziglesias

Neuroscience is my principal interest. I want to understand how neurons and
neuronal circuits perform computations and result in behavior. As a
researcher in computational biology (from a biochemistry background), I had
almost no formal training in programming. As such, during my PhD and part
of my postdoc, I committed all of the sins common in academic software:
more scripts than functions, no version control, no tests, and so on.

By the start of my postdoc I *was* making an effort to write good software.
I was lucky enough that my image segmentation library, Gala, was accepted
for a talk at the SciPy 2012 conference. That event changed my life and my
approach to software. Stéfan van der Walt, creator and lead developer of
the popular scikit-image library, invited me to participate in the sprint,
where I would make my first-ever GitHub pull request.

Today, I am a core developer for scikit-image, and (most) of my software
has at least *some* tests. I write regularly about good software
development practices on my blog, I Love Symposia. And I hope to set a good
example by mentoring younger students, for example as a mentor for the
Google Summer of Code '14.

### Author Web site/blog/Twitter: 

[http://ilovesymposia.com](http://ilovesymposia.com), 
[@jnuneziglesias](https://twitter.com/jnuneziglesias), 
[Github: jni](https://github.com/jni)

[http://mentat.za.net](http://mentat.za.net), 
[@stefanvdwalt](https://twitter.com/stefanvdwalt), 
[Github: stefanv](https://github.com/stefanv)

[Harriet Dashnow Researcher page](https://www.vlsci.org.au/researcher/hdashnow), 
[@hdashnow](https://twitter.com/hdashnow), 
[Github: hdashnow](https://github.com/hdashnow)

### Why are you the best person to write this book?

I only recently ascended the software developer ladder from "lowly academic
hack" to "core dev of a major scientific library". As such, I understand
what it feels like to not know what "test-driven development", "continuous
integration", "cache misses", or even "NumPy array" mean. This places me in
a prime spot to guide new programmers through this.

I'm very passionate about teaching, and about good writing.

Finally, reviewing code for scikit-image pull requests, I've developed an
eye for what great code looks like. Some examples will be from those pull
requests, but the majority will come from polling developers from the
Scientific Python ecosystem, many of whom I know personally from two SciPy
conferences, EuroSciPy 2013, and PyConAu 2014.

Stéfan van der Walt is the creator of the scikit-image library, and a frequent
contributor to SciPy and other scientific libraries, and has organised
several of the SciPy conferences. His breadth of knowledge eclipses mine and
will help to develop many of the chapters.

Harriet Dashnow is a bioinformatician and an excellent writer. (See, for
example, her hilarious [Ten Simple Rules for Writing a PLOS Ten Simple Rules
Article](http://www.ploscompbiol.org/article/info%3Adoi%2F10.1371%2Fjournal.pcbi.1003858).)
She recently started using Python and is thus part of the target audience for
the book.

## Book Summary:

### In one sentence, tell us why the audience will want to buy your book.

Scientists seeking to take their Python to the next level will want to learn by
example from the very best code.

### Summarize what the book is about, like you would pitch it to a potential reader on the back cover.  What makes your book unique in the marketplace?

NumPy and SciPy form the core of the Scientific Python ecosystem. They also
have excellent online documentation, so a complete reference would be
pointless. Instead, we present the best code using these libraries,
using it as motivation to teach readers who have never used them before.

The examples will be chosen to highlight clever, elegant uses of advanced
features of NumPy, SciPy, and related libraries. The beginning reader will
learn not the functionality of the library, but its application to real
world problems using beautiful code. The book will start from first principles
and provide all the necessary background to understand each example,
including idioms, libraries (e.g. iterators), and scientific concepts. Examples
will use actual scientific data.

This book will introduce readers to Scientific Python and its community, show
them the fundamental parts of SciPy and related libraries, and give them a
taste for beautiful, easy-to-read code, which they can carry with them to their
practice.

### Briefly explain the technology and why it is important.

The SciPy software library implements a rather disjointed set of scientific
data processing functions, such as statistics, signal processing, image
processing, and function optimization. It is built on top of the numerical
array computation library NumPy. On top of these two libraries, an entire
ecosystem of apps and libraries has grown dramatically over the past few years
(see the "how many people will use this technology" section), spanning
disciplines as broad as astronomy, biology, meteorology and climate science,
and materials science.

This growth shows no sign of abating.  The Software Carpentry organization,
which teaches Python to scientists, currently cannot keep up with demand, and
is running "teacher training" every quarter, with a long waitlist. (I am
enrolled in the current session, finishing this year.)

In short, SciPy and related libraries will be driving much of scientific data
analysis for years to come.

## Audience:

### Explain who the primary audience is for your book. What skills can you assume they have mastered?

A reader should be familiar with the Python programming language. There should
be no other requirements to understand the book. We have two key audiences,
who have similar levels of experience and understanding:

 1. Those fresh out of a Software Carpentry Python tutorial. They signed up
    because they want to do more sophisticated things with their data than
    software such as Excel allows. They have seen Python, and have ideas about
    variables, functions, loops, and even a bit of NumPy, but they don't know
    about the SciPy stack and they certainly don't know best practices, how easy
    it is to join the community and contribute, etc.
 2. The self-taught scientists. (This was me once upon a time.) They have read
    some Python tutorials online, and have downloaded some analysis scripts from
    another lab or a previous member of their own lab, and have fiddled with them.
    But they don't have any solid concepts about what constitutes "good code".

(A secondary audience is the more advanced practitioners of scientific Python
programming, who might be interested in the advanced examples motivating each
lesson. After all, I fall into this category and the examples will be chosen
because I and similar programmers find them beautiful and insightful.)

### Please estimate as best you can how many people will use this technology? Please state any applicable statistics (e.g., web searches, web site traffic, blogs) indicating market use or market growth.

I think O'Reilly is in a better place to answer this question, but regardless
of absolute numbers, they are certainly increasing dramatically. For example,
see this plot by Chris Beaumont, an astrophysicist at Harvard:

![Python v IDL](https://pbs.twimg.com/media/By43l0FIEAEJ0E6.png:large)

(Source:
[Twitter](https://twitter.com/BeaumontChris/status/517412133181865984).
Code: [NBViewer](http://t.co/NwzzReuzfe).)

The SciPy conference has also grown dramatically over the past few years.

### Please provide some scenarios that indicate how the audience will use your book. For example, will readers refer to it daily as a reference? Will they read it once to learn the concepts and then refer to it occasionally?

This will not be a reference volume. As I mentioned, the internet now provides
a far better reference than any book could, especially considering the rapid
pace of development in this field. Instead, a reader will learn the core
concepts and capabilities of SciPy and related libraries by reading once, but
may well return for inspiration to the final code examples themselves.

## Key Topic Coverage:

### What problems does this book solve for its users?

Many scientists and beginning programmers have learned basic Python
programming, for example via Software Carpentry, online tutorials, or any
of a number of massive open online courses (MOOCs). They may, however, struggle
to apply this basic programming skill to more complex problems in their
scientific domain.

The SciPy library, and the ecosystem that has grown around it, are there for
this purpose, but finding useful functions and using them correctly,
efficiently, and in easily readable code are two different things. Readers will
be able to learn by example from some of the best code available, selected to
cover a wide range of SciPy and related libraries. (These include scikit-learn,
scikit-image, toolz, and pandas.)

Thus the book aims to point readers in the direction of excellent code in the
scientific domain. For its core audience of recent Software Carpentry graduates
and self-taught learners, the book will:

1. Introduce them to Scientific Python and its community.
2. Show them the most fundamental parts of SciPy and related libraries, while
   showing some of the principles of writing good, robust software.
3. Give them a taste of beautiful, easy-to-read code, which hopefuly they will
   carry with them to their practice.

Advanced readers may discover new, refreshing ways of looking at the
libraries they use every day.

### List the four or five topics covered or features included that will provide the greatest benefit to readers or will be the most likely to excite them? 

The SciPy community (preface). Sounds dry but will include nice touches such as
good package names, such as airspeed velocity and sux.

n-dimensional image processing (includes numpy array memory representation,
filters, processor cache and efficiency), Fourier transforms, streaming data
processing (toolz), sparse matrices.

Contributing to open-source projects in the SciPy ecosystem.

## Other Book Features and Video Offerings:

### Is there a companion web site? If so, what do you plan to include on the site? Would you be willing to participate in video offerings as well as workshops and training seminars?

I'm not sure how much O'Reilly would be comfortable with me putting on a
companion site, but I would ideally like to have IPython Notebooks
corresponding to each chapter so that readers can modify and play with the code
to their heart's content.

I would certainly be willing to participate in video workshops and seminars,
and have done so for example in the scikit-image tutorial at SciPy 2014, which
was extremely successful, recorded, and posted on YouTube.

## Competition:

### What books or online resources compete with this book? Please list the title and author. In each case, how will your book be different or better in timing, content, coverage, approach, or tone?

The online documentation for SciPy, and blogs, are the biggest competition
here. The SciPy community is becoming large enough that there are plenty of
resources online to learn about using it. There are three key differences
between this book and what you can get from online tutorials:

 - Reference guides, such as the
   [SciPy reference](http://docs.scipy.org/doc/scipy-0.14.0/reference/), tell
   you about the inputs and outputs of individual functions, but do not provide
   a good idea about how to compose those functions together to achieve a
   scientific goal.
 - Blog posts are often aimed at someone of similar skill level as the writer.
   This book will ensure that each chapter is interesting to novices and
   advanced readers alike.
 - Blog posts vary widely in quality; this book will be carefully curated and
   proofread to ensure only the highest quality code is included.

Several books have addressed the use of Python for scientific data analysis.
Examples include Pandas, Astropy, PyMCMC. Those books are much more focused
to specific tasks. Here, we instead aim for broad coverage of SciPy.

## Book Outline (chapter level is fine):

The goal of this book for the reader is to fast track them through high-quality
code. Their reaction with the first example might be "Wow, I'd never be
able to come up with that." But, by the time they have finished the book, they
should find each example still very clever, yes, but something that they
themselves could have written in an inspired moment.

Except for the Preface and Chapter 1, the below chapters are intended as a
guideline.

*Preface:* why SciPy? Ecosystem and community. Conventions (e.g. NumPy docstring
conventions).

*Chapter 1:* Image segmentation using `ndimage.generic_filter`. This includes
an introduction to the NumPy array, memory layout, strides, F- and
C-contiguity, 1D, 2D, and nD filters, and finally filtering to produce a graph
and segmentation from that graph. (This may be broken down into several
smaller chapters.)

*Chapter 2:* Fourier Transforms. (Need to find a killer application/use for
this one, but it's a central enough topic that it will be a high priority to
include such an example.)

*Chapter 3:* Use of sparse matrices to evaluate clustering accuracy.

*Chapter 4:* Eigendecomposition. (Same as FTs.)

*Chapter 5:* Optimization. (idem)

*Chapter 6:* Streaming data. (idem, but specifically want to include use of
Matt Rocklin's Toolz)

*Chapter 7:* Basic statistics.

... Perhaps additional chapters with awesome examples using scikit-learn,
scikit-image, pandas, astropy, etc. The exact contents will be determined by
code submissions, which will be triaged to canvas as wide a footprint of SciPy
as possible.

*Chapter -1:* Contributing to the SciPy ecosystem: how to use git and github,
and follow best practices, to contribute to SciPy and related packages.

## Specs and Schedule:

### How many pages do you expect the book to be?

200-250 pages.

### How long do you expect it to take you to write the book?

About 9 months.

The book will be written as IPython notebooks in a public repository and we
will request feedback during writing from key audiences (to which we have ready
access, since we all teach Python/SWC relatively frequently), ensuring that the
book meets the needs of its intended audience.
