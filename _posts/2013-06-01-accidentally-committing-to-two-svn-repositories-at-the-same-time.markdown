---
comments: true
date: 2013-06-01 13:15:00
layout: post
slug: accidentally-committing-to-two-svn-repositories-at-the-same-time
title: How I Accidentally Commited to Two Subversion Repositories At The Same Time
summary: 'Otherwise known as "Subversion I Hate You..."'
image: 'accidentally-committing-to-two-svn-repositories-at-the-same-time/svn.jpg'
tags:
- php
- work
- development
- subversion
- version control
---

For certain reasons, reasons I won't go into in the blog post, I'm stuck using Subversion again. For the time being anyway until we have enough time to execute an escape plan! An interesting bug recently taught me a few new interesting thing about Subversion.

Now, the last time I used Subversion was several revisions, and many years, ago. Back then the preferred method for Subversion to keep track of files and folders appeared to be putting a .svn folder within every sub directory. The new kids on the block, Git and Mercurial, demonstrated what a stupid idea this actually was.

So picture this, you're working on a rather large refactor of some site-wide code. You're working in a new branch as you would expect. Because you actually work in the real world and not in some unachievable, imaginary, perfect world you also have to deal with bug fixes and feature requests in the current trunk too. But that's fine, you commit regularly as this branch is yours and yours alone so switching back to trunk and tweaking some stuff is all good. You then just switch back to your development branch and carry on your super cool refactor! Still committing regularly as you go along. Until... WTF? The staging area, that runs off trunk, is broken! How the hell!?

This is actually how this happened by the way. Upon further investigation I found that some of my code from my refactor had found its way into trunk. I initially thought that maybe I'd forgotten to switch back to my refactor branch after tweaking some stuff in trunk, but that was impossible, I would have noticed that all my other refactor code was missing. Then I stumbled on the rogue commit responsible, but what I was seeing made no sense at all.

![SVN commit log showing the rogue commit](/img/posts/accidentally-committing-to-two-svn-repositories-at-the-same-time/svn_commit_log.png "The rogue svn commit")

What in the holy fuck is that? So in a single commit I managed to commit half of the modified files to my refactor branch, and the other half to our DMZ branch which gets merged into our trunk when we do a deployment... How the hell does that even happen?

Well, the answer used to be that the .svn folder within the sub folder those files reside in had been copied from another project and thus contained the repository path for the second repo. However, a quick search around the codebase revealed that Subversion had changed their tactics and were now using an SQLite database instead of a folder per sub folder. A much more sensible solution. But it still didn't answer my question.

[SQLiteman] [1] to the rescue! The database containing all of the information about a Subversion repository is stored in the root .svn folder and is the wc.db file. I opened this in SQLiteman and ran the node_base view. I was treated to a view similar to the image below, unfortunately I don't have the screenshot that I took anymore, but this will illustrate the point just fine.

![SQLiteman view of the SVN database](/img/posts/accidentally-committing-to-two-svn-repositories-at-the-same-time/sqliteman.png "SQLiteman view of the SVN database")

Somehow in the repos_path of the affected files it referenced the refactor branch for some of the files and the dmz branch for others. The only thing I can this of is that Subversion (more importantly TortoiseSVN) threw some kind of shit fit during all of the switching and I either didn't see the error (more likely) or Subversion didn't report an error and half of my repo stay on dmz whilst the other half switched to my refactor branch.

Needless to say, I now check the path of every file when I'm doing a commit.

[1]: http://sqliteman.com/ "SQLiteman"