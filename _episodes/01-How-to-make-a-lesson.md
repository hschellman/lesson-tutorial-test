---
title: How to make a Lesson for DUNE
teaching: 30
exercises: 0
questions:
- How can I make a lesson like this from scratch using the DUNE template
objectives:
- Learn how to set up locally to build a lesson and to deploy it.
keypoints:
- If you can do basic markdown, you can do this. 
---


## Here I describe how I built this lesson.  You can follow along. 



> #### Note:  
> Check out the [previous episode]({{ site.baseurl }}/00-Local-Setup-For-Local-Build.html)to set up a local server and to do local builds. 
{: .callout}

## First you need to decide on a name for your new lesson. 

> #### Note: 
> Because github insists on using gh_pages for deployment, it is good to use your own github account for initial (and ongoing) development and pull over to /DUNE/ for the official version rather than using branches in the /DUNE/ github area.
{: .callout}

## Do local setup for local rendering (optional)

Then follow the instructions [https://carpentries.github.io/lesson-example/setup.html#setup-for-local-rendering-of-the-lessons-optional](https://carpentries.github.io/lesson-example/setup.html#setup-for-local-rendering-of-the-lessons-optional) for setup on your local machine - in principle this is optional but in practice it is really helpful.  You are going to need ruby and pyYAML.  I used conda on a mac but they have instructions for Windows, Mac and UNIX. 

> #### Alert!!! 
> At this point you should stop following their instructions and start using our template to avoid overwriting DUNE specific items. 
{: .callout}

## Then import this template. 

- Use the [GitHub’s importer](https://github.com/new/import) to make a copy of this repo in your own GitHub account. (Note: This is like a GitHub Fork, but not connected to the upstream changes)

- Put the URL of this repository, that is https://github.com/DUNE/lesson-template.git in the “Your old repository’s clone URL” box. 

- Select the owner for your new repository (you). 

- Set the name you chose for your lesson repository. 

- Make sure the repository is public.

> #### Note: 
> Please import to your own account and new lesson, work there and then move it over to `/DUNE/` once you have a decent draft in place. 
{: .callout}


The difference from the carpentries is the addition of the DUNE logo and stuff specific to our lessons.  


## now make a local copy on the gh-pages branch and edit away
~~~
git clone -b gh-pages <your new repository>
~~~
{: .language-bash}

You need to look at the following pages.

- `_config.yml ` to set the title and other parameters for the lesson
- `AUTHORS` to tell people who is doing this
- `CITATION` how to cite the page - often just the URL
- `LICENSE`  you can keep it as is
- `LICENSE.md` 
- `README.md`
- `reference.md`
- `setup.md` This is currently the full setup for new users. 

Then throw your individual modules into `_episodes` with leading numbers to set the order.  The code will follow the ordering of the files in `_episodes`.  

There are very nice examples and a formatting tutorial at: [https://carpentries.github.io/lesson-example/](https://carpentries.github.io/lesson-example/)

All lessons need to have a header that describes them

~~~
---
title: How to make a Lesson for DUNE
teaching: 30
exercises: 0
questions:
- How can I make a lesson like this from scratch using the DUNE template
objectives:
- Learn how to set up locally to build a lesson and to deploy it.
keypoints:
- If you can do basic markdown, you can do this. 


... body of the lesson ...

~~~

{: .source}

In particular, check out 

- [Organization](https://carpentries.github.io/lesson-example/03-organization/index.html)
- [Formatting](https://carpentries.github.io/lesson-example/04-formatting/index.html)
- [Style Guide](https://carpentries.github.io/lesson-example/06-style-guide/index.html)

You can throw supplemental stuff into `_extras`.

## You can then build your site locally either as a server or just a local site.

### local site

~~~
make site
~~~
{: .language-bash}

This does a lot of setup - it's pulling in a lot of ruby "gem" files. 

Your local site will be in _sites/index.html

#### Checking

~~~ 
make lesson-check
~~~
{: .language-bash}

will tell you about all the FIXME's you haven't fixed and missing formatting syntax.

### local server

~~~ 
make serve
~~~
{: .language-bash}

will launch a web server and a site at: `http://127.0.0.1:4000`  

You may need to reload the web site to see your changes. 

> ### Note: 
> These will hang around until you kill them so if you try to launch twice you can't. Look for processes with:
{: .callout}


~~~
ps -ef | grep jekyll
~~~
{: .language-bash}

### Publishing your draft site to `<yourname>.github.io/<yoursite>`

Ok, so now you should be able to push your site to github.io

We have provided a `gitadd.sh` script that adds the most common **source** files so you don't mistakenly publish all of the html you just generated.

~~~
# make certain you're up to date with the main repo
git pull
# make certain you are in your gh-pages branch
source gitadd.sh
git commit -m " I DID SOMETHING"
git push
~~~
{: .language-bash}

Wait a couple of minutes and you shouild see your page appear at:

`https://<yourname>.github.io/<yoursite>`


Ok, once you have your site in decent shape you can import it back to

`https://github.com/DUNE/<yoursite>`

### Making it official

Once you have it checked out you can use the import function to make an official dune site.

- Use the [GitHub’s importer](https://github.com/new/import) to make a copy of this repo in your own GitHub account. (Note: This is like a GitHub Fork, but not connected to the upstream changes)

- Put the URL of this repository, that is `https://github.com/<yourname/<yoursite>.git` in the “Your old repository’s clone URL” box. 

- Select the owner for your new repository `DUNE`

- Set the name you chose for your lesson repository `<yoursite>`

- Make sure the repository is public.

### Maintaining your site

- try to make changes on your local copy - others can also do things in their local copies

- use pull requests to merge changes into the official DUNE site where possible

- you can make minor patches directly on the main site but generally, it's better to work locally. 

