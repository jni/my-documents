# Some things I learned while building a site on GitHub Pages

Understatement: I'm not much of a web developer. However, we all have to become
a little bit versed in web-dev if we want to publish things these days. GitHub
Pages makes it really easy to publish a site (check out the
[official guide](https://pages.github.com) and Thinkful's truly excellent
[interactive getting started guide](http://www.thinkful.com/learn/a-guide-to-using-github-pages/)).

If you just want to publish a static set of html files using absolute paths,
you'll be fine. However, Pages uses [Jekyll](http://jekyllrb.com), a server
that can transform collections of Markdown, HTML, and other files into 
full-fledged websites.
The process is definitely full of gotchas, though, and you'll run into issues
for anything other than single pages. I'm making this list for my own future
reference, and so that I can finally close the umpteen tabs I have open on the
topic. =P But I hope someone else will find it useful!

## 1. Jekyll lets you write Markdown, but it's not GitHub-Flavored Markdown

You might assume, since you are writing markdown hosted on GitHub, that
[GitHub-Flavored Markdown (GFM)](https://github.github.com/github-flavored-markdown/)
would work. But you would be wrong. You can
configure Jekyll on GH-Pages to use either
[Redcarpet](https://github.com/vmg/redcarpet)
or [Kramdown](http://kramdown.gettalong.org/syntax.html), both of which have
significant syntactic differences with GFM. For example, fenced code blocks
[use `~~~` in Kramdown](http://kramdown.gettalong.org/syntax.html#fenced-code-blocks),
instead of GFM's `` ``` ``. 

Anyway, to set the Markdown engine used to render your site, set the `markdown`
attribute in the Jekyll configuration file, `_config.yml`, placed at the root
of your repo:

```yaml
# Dependencies
markdown:    kramdown
highlighter: pygments
```

## 2. ... And syntax highlighting doesn't work properly in Jekyll on GH-Pages

Even using the correct delimiters for Kramdown is not good enough to get your
code snippets to render properly, because of
[this](https://github.com/jekyll/jekyll/issues/2709) and
[this](https://github.com/jekyll/jekyll/issues/2715). So, instead of using
backtick- or tilde-fenced blocks, you have to use slightly clunkier Jekyll
"liquid tags", which have the following fairly ugly syntax:

```markdown
{% highlight python %}
    from scipy import ndimage as nd
{% endhighlight %}
```

## 3. Linking is a bit weird

My expectation when I started working with this was that I could write in
markdown, and link directly to other markdown files using relative URLs, and
Jekyll would just translate these to HTML links when serving the site. This is
how [MkDocs](http://www.mkdocs.org) and local viewers such as
[Marked 2](http://marked2app.com) work, for example.

That's not at all how Jekyll does things. **Every markdown page that you want
served needs to have a header called the
[Front Matter](http://jekyllrb.com/docs/frontmatter/).** Other markdown files
will be publicly accessible but they will be treated as plaintext files.

*How* the markdown files get
served also varies depending on your `_config.yml` and the
[`permalink` variable](http://jekyllrb.com/docs/permalinks/). The annoying
thing is that the documentation I just linked to is entirely centred on blog
posts, with little indication about what happens to top-level pages. In the
case of the `pretty` setting, `filename.markdown`, for example, gets served at
`base.url/filename/`, *unless* you set the page's `permalink` attribute
manually in the Front Matter, for example as `title.html` or `title/`.

## 4. Relative paths don't work on GH-Pages

This is a biggy, and super-annoying, because even if you follow GitHub's
[guide for local development](https://help.github.com/articles/using-jekyll-with-pages/),
*all* your style and layout files will be
missing once you deploy to Pages.

The problem is that Jekyll assumes that your site lives at the root URL (i.e.
`username.github.io`), when it is in fact in `username.github.io/my-site`.

The solution was developed by [Matt Swensen](https://github.com/mjswensen)
[here](https://github.com/jekyll/jekyll/issues/332#issuecomment-18952908): You
need to set a `baseurl` variable in your `_config.yml`. This should be your
repository name. For example, if you post your site to the `gh-pages` branch of
the repository `https://github.com/username/my-jekyll-site`, which gets served
at `username.github.io/my-jekyll-site/`, you should set `baseurl` to
`my-jekyll-site`.

Once you've set the `baseurl`, you *must* use it when linking to CSS and posts,
using liquid tags: `{{ site.baseurl }}/path/to/style.css` and
`{{ site.baseurl }}{{ post.url }}`.

When you're testing the site locally, you can either manually configure the
`baseurl` tag to the empty string (`bundle exec jekyll serve --baseurl ''`), so
you can navigate to 0.0.0.0:4000 as you would normally with Jekyll; or you can
[leave it untouched](http://blog.parkermoore.de/2014/04/27/clearing-up-confusion-around-baseurl)
and navigate to 0.0.0.0:4000/my-jekyll-site, mirroring the
structure of GitHub Pages.

**This is all documented in a specific Jekyll docs page** that is unfortunately
buried after *a lot* of other, less-relevant Jekyll docs. As a reference, look
[here](http://jekyllrb.com/docs/github-pages/), and search for "Project Page
URL Structure".

## 5. You *must* provide an index.html or index.md file

Otherwise you get a rather unhelpful
[Forbidden Error](https://github.com/jekyll/jekyll/issues/1293).

## And 6. There is a "console" syntax highlighter for bash sessions

I'd always used "bash" as my highlighter whenever I wanted to show a shell
session, but it turns out that "console" does a slightly better job, by
highlighting `$` and `>` prompts and commands, while graying output slightly.
Christian Jann, who has written his own more-specific highlighter,
ShellSession, has a
[nice comparison](http://www.jann.cc/pygments-shell-session-lexer-demo/shell_code_comparison.html)
of the three. Although ShellSession is cool, I couldn't get it to work
out-of-the-box on Jekyll.

***

That should be enough to get you started... (Don't forget to check out
[Thinkful's guide](http://www.thinkful.com/learn/a-guide-to-using-github-pages/)!)
Happy serving!
