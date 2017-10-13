<!--
.. title: Switching to Nikloa for Jupyter Notebooks and a static site
.. slug: switching-to-nikloa-for-jupyter-notebooks-and-a-static-site
.. date: 2017-10-12 13:52:49 UTC
.. tags: 
.. category: 
.. link: 
.. description: 
.. type: text
-->

I've been using WordPress for quite a while, almost entirely because it's an out-of-the-box blog setup that just works. But it kind of sucks for what I mostly want to do, which is stick some code into blog posts. In fact, what usually happens is that I do something in a Jupyter notebook, and want to stick it up as a blog post. That's a real pain in WordPress. The best I found was converting the notebooks to html and then including them as a static block, but those invariably are brittle and ugly.

So, smart people like [Jake Vanderplas](http://jakevdp.github.io) and [themodernscientist](http://themodernscientist.com) switched over to something that deals natively with Jupyter notebooks a long time ago (so long ago they were called IPython Notebooks!). I'm a slow pony, but I'm switching to Nikola. It seems to be the easiest one at the moment. It's a static page generator, which is more than fine for my purposes, and it deals natively with Jupyter notebooks. Sweet. I thought it would be useful to document the process for future-me. I leaned heavily on the Nikola site (including the [documentation for import_wordpress](https://getnikola.com/handbook.html#importing-your-wordpress-site-into-nikola)). The process wasn't completely trivial, but that's because I did some hacky stuff to get Jupyter Notebooks included in my WordPress posts anyway. This seems like a lot of work for like 13 posts, but nobody ever claimed I was wise.

## Grabbing the site

Log in as an administrator, go to the Tools menu, click on Export, then download an Export File. Nice and easy. Thanks, WordPress!

## Install Nikola

*Note:* `pip` doesn't actually play nicely with the conda environments. It looks like it installs nikola's stuff on top of everything else (e.g. the Nikola tools are available even when I'm not in the `blog` environment from below). That's not great. I probably should use a virtualenv, but I don't have time to learn what one of those is today.

I'm using Anaconda for my Python, and Nikola installs via pip, so I make a new environment just for the blog. Probably good practice anyway. Speaking of which, this is all Python 3. There's some [weird bug](https://github.com/ContinuumIO/anaconda-issues/issues/542) involved in having pip upgrade setuptools, 

```shell
conda create --name blog
source activate blog
conda install setuptools
pip install --upgrade "Nikola[extras]"
mkdir blog
cd blog
mkdir posts
mkdir output
```

Now import the wordpress site. If I just say

```shell
nikola import_wordpress ~/Downloads/biophysicsandbeer.wordpress.2017-10-10.xml
```

I don't actually get some of my content imported. In particular, the quoted Python code doesn't show up. So,

```shell
nikola import_wordpress --download-auth=[my secret username]:[my secret password] --install-wordpress-compiler --transform-to-html ~/Downloads/biophysicsandbeer.wordpress.2017-10-10.xml
```

Tells it to be explicit about converting to html and downloading everything it can. It also produces some errors, specifically a bunch of lines like

```
[2017-10-11T19:49:10Z] WARNING: Nikola: Can't do a redirect for: 'http://www.mglerner.com/blog/?p=8/'
```

which are telling us that it can't just spit out a new file in place of the old one because the question marks in the URL mean request data. We'll deal with this in a minute.

We then fire up the site with

```shell
cd new_site
nikola build
nikola serve --browser
```

And it almost all works. Here are the missing things:

###My pre-rendered Jupyter notebooks suck.

I used the pageview WordPress plugin (short code? I don't know) to include pre-rendered Jupyter notebooks. That just breaks upon import. But the Nikloa posts are just straight HTML. I can just include the stuff directly. That was pretty easy. In my future free time (ha!), I might go back and convert some of them directly to Jupyter notebooks.

###Comments are all missing.

1. For future stuff to work, I'll get a Disqus ID and start using it. (biophysics-and-beer ... check).

2. Add all of the old comments by hand. This isn't taking a huge amount of time, because I don't have a huge amount of comments, and I'm not going crazy with matching formatting. I'm just copying the comments div from the old blog. If you're doing this to your own blog, don't forget to get rid of the "response" part of the comments div. If I had it to do over, I'd write a script that did that for me, or I'd learn how to import comments into Disqus, but it didn't take much time this way. On the plus side, I'm ditching some (not all) spam I had missed.


## Getting a graphical header/theme fun time

I found the [Nikola tutorial for theming](https://getnikola.com/creating-a-theme.html) ... somewhat more than I was
interested in. But, it had enough useful nuggets to figure out the
basics. The basic idea is (1) put my header image somewhere (2) edit
the header template. Let's go.

First, I'm going to want to change the `base_header.tmpl` so I
searched for themes that came with that on the
[Nikola Theme site](https://github.com/getnikola/nikola-themes/find/master). Of
those, I like `jidn` the most. So,

```shell
nikola theme -i bootstrap3-gradients
```

Then edit `conf.py` to switch the theme to jidn and, as indicated in
the text when you install the jidn theme, add a few lines to `conf.py`

```
THEME = "jidn"
...
GLOBAL_CONTEXT.update({
    "JIDN": {},  # Extra info about authors
    # "JIDN-theme": "theme-base-blue",
})
...
```
(Actually, as described in the jidn README.md, you can add more info
to that dictionary, so I added a link to my twitter profile image,
etc. Neat.)

The WordPress import stuck all of the versions of my header in
`files/blog/wp-content/wp-content/uploads/` and I'm just copying them
to `files` to make them easy to find. Then I add the `img` tag right
after the title in `themes/jidn/templates/base_header.tmpl`:

```
    <h2 id="brand" class="masthead-title">
      <a href="${abs_link(_link("root", None, lang))}" title="${blog_title}" rel="home">${blog_title}</a>
    </h2>
    <img src="/mglblogheader.png" />
```

I'm very far from up-to-date with modern web
design, but that looks OK for now.

While I'm editing the templates,
there's a link to "blog" in the sidebar I don't want, so I replaced it
with a link to the about page.

## Back to the redirects

Those redirects are kind of a pain. That's Nikola saying it can't just spit out a new file in place of the old file because the question marks mean request data. Thanks, wordpress! I wanted simple stuff like an `.htaccess` file saying

```
Redirect /blog/page8 /blog/new-and-fancy.html
```

but no ... Now I need to look at a [StackOverflow answer](https://stackoverflow.com/questions/9182585/apache-redirect-permanent-for-url-with-data-in-string-question-mark) and remember why I stopped being a web developer years ago. Here's my new `.htaccess` file

```
RewriteEngine on
RewriteBase /

RewriteCond %{THE_REQUEST} ^[A-Z]{3,9}\ /blog/\?p=5/ [NC]
RewriteRule ^ /blog/posts/the-blogging-begins.html [L,R=301]
RewriteCond %{THE_REQUEST} ^[A-Z]{3,9}\ /blog/\?p=5 [NC]
RewriteRule ^ /blog/posts/the-blogging-begins.html [L,R=301]
```

to handle people accessing each page both with and without a trailing slash. Now, where should I point the redirects?

## Static site means why host it myself?

It made sense to host my own WordPress site. But I'm not sure I need to host my own static site. In fact, life would probably be easier if I just used  github pages. Cool.  Github has [instructions](https://pages.github.com) that basically boil down to "set up a repo called mglerner.github.io and do some special things" ... and Nikola means I don't have to actually know what those special things are! After initializing my Nikola blog directory as a github repo and doing

```shell
git remote add origin git@github.com:mglerner/mglerner.github.io.git
```

I can make Nikola rebuild things like github wants, add, commit and push everything automatically with

```shell
nikola github_deploy
```

So, after having done that, I just make the `.htaccess` file listed above point everything from my old site to my fancy new github site.

... and it's up and running!

## Making it possible to post with Jupyter notebooks

This is documented in a few places, but sometimes things change, so
you're probably better off just looking at the Nikola site
directly. At the moment, you need to add the last line here to each of
`POSTS` and `PAGES` in `/blog/conf.py`, so that Nikola will recognize
Jupyter notebooks as ... you know ... both posts and pages. You also
need to add the trailing line in `COMPILERS`.

```python
POSTS = (
    ("posts/*.rst", "posts", "post.tmpl"),
    ("posts/*.txt", "posts", "post.tmpl"),
    ("posts/*.md", "posts", "post.tmpl"),
    ("posts/*.html", "posts", "post.tmpl"),
    ("posts/*.ipynb", "posts", "post.tmpl"),
)

PAGES = (
    ("pages/*.rst", "pages", "story.tmpl"),
    ("pages/*.txt", "pages", "story.tmpl"),
    ("pages/*.md", "pages", "story.tmpl"),
    ("pages/*.html", "pages", "story.tmpl"),
    ("pages/*.ipynb", "pages", "story.tmpl"),
    )

COMPILERS = {
    "rest": ('.txt', '.rst'),
    "markdown": ('.md', '.mdown', '.markdown'),
    "html": ('.html', '.htm'),
    "ipynb": ('.ipynb',),
}

```

## Making posts

Now comes the whole point: making new posts. Blog posts come with meta data (when it was created, etc.) that normally gets automatically handled when you create a new post via `nikola new_post -e`. If you want to start with other formats (e.g. Markdown or Jupyter notebooks), you just stick the relevant file in `/posts` and import it via `nikola new_post -i`.

I took the notes for this migration in Markdown, so I just stick that
file in `/posts/BlogMigration.md` run `nikola new_post -i
posts/BlogMigration` ...


Or, at least, that's how it should work. I'm a little disappointed to find that the new post import keeps breaking, saying it can't find metadata like the date. It's an easy workaround for markdown: I just make a new post, then copy over my markdown. Looking at the results, I find that Nikola wants the metadata imbedded in the markdown file. So, I should have started the markdown file with

```
<!--
.. title: Switching to Nikloa for Jupyter Notebooks and a static site
.. slug: switching-to-nikloa-for-jupyter-notebooks-and-a-static-site
.. date: 2017-10-12 13:50:23 UTC
.. tags: 
.. category: 
.. link: 
.. description: 
.. type: text
-->
```

Cool. I tested, and I can indeed just stick that at the top of my
markdown file (which I'm storing in a folder called `drafts`) and then
import. Almost. Of all things, it sticks that metadata in twice. So,
for now, the clear answer is just to make a blank post and then copy
in my markdown. Easy enough.

Meanwhile, importing Jupyter notebooks seems to just work!

then `nikola build`, then fire up a test server to check it out with `nikola serve --browser`, verify that all looks awesome, and push it to the blog with `nikola github_deploy`! 

##TODO

 * The twitter follow plugin doesn't work. I think that should be
   straightforward, but I'll fix it later. 
 * The text is too big. I can apparently change that in `jidn`'s
   `custom.css` but I don't quite get how.
## Jupyter issues

The conversion of Jupyter notebooks doesn't look perfect yet:

* Inline math (starting with a single dollar sign) doesn't always get
  converted. Starting with two dollar signs does seem to consistently
  work.
* For JSAnimations, the "animation bar" doesn't have images on the buttons.
