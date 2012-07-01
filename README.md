# Symfony2 Simple Deploy Scripts

## Background

Getting started with Symfony2 can be a daunting task for those of us new to it and one of the areas that
I found the most confusing, was how to properly deploy a project to various servers.

_Should I be using_:

+ Capifony?
+ git push/pull to remote?
+ Some pre-built Deploy Bundle?
+ rsync?
+ ssh?

Although project deployment seems to be a critical & fundamental part of any Symfony2 project, there didn't
seem to be any consensus as how best to go about this. As I couldn't find any gentle introduction to the
subject, I decided to put this together in the hopes that it will make this easier for others following in
my footsteps.

_I'm still learning both Symfony2 and how best to deploy, so please let me know if you find a mistake or
a missing step or two_ :-)

__Tip__:
If you're doing your development work in Windows and want to build Symfony2 based projects, do yourself
a huge favour and install VirtualBox (or similar) and put your project on a Linux of your choice. It makes
everything smoother (well, once you've learned how to build a LAMP server!)


### Capifony
I found Capifony to be interesting, but rather opaque (not a lot of docs and still not quite sure
how to use it even after I got it all working). I don't know Ruby and the thought of having
to dig through yet-another-language to be able to follow along didn't appeal greatly (and I found Ruby a
royal pain to install properly!).

+ http://capifony.org/
+ https://github.com/everzet/capifony


### git
At first I thought it would be slick to have git handle deploying directly to my servers with
some sort of post commit hook. Turns out that this really isn't that simple (at least if your
a mere git mortal like myself). In the end I decided to just use git for what it was designed for
(version control/branching) and not muddy the waters by trying to get it to manage my deploys as well.

_Here are some articles that discuss ways to deploy via git_:

+ http://toroid.org/ams/git-website-howto
+ http://ikiwiki.info/rcs/git/
+ http://joemaller.com/990/a-web-focused-git-workflow/
+ http://ryanflorence.com/deploying-websites-with-a-tiny-git-hook/
+ http://deadlytechnology.com/web-development/deploy-websites-with-git/
+ http://www.markdotto.com/2011/11/02/how-to-deploy-sites-via-github/
+ http://philsturgeon.co.uk/blog/2010/02/Deploying-websites-with-Git



### Deploy Bundle(s)
I then looked at the handful of Symfony2 Bundles that have been built to handle deployments.
I quickly discovered that they are all just wrappers around rsync and ssh. Inevitably getting
a solid deploy concept working means having to tweak things for your specific needs -- having the
various linux commands burried in a Symfony2 php bundle just made it tough for me to understand and
modify to suit my needs.

+ http://knpbundles.com/aerialls/MadalynnPlumBundle
+ http://knpbundles.com/dator/DeployBundle
+ https://github.com/BeSimple/BeSimpleDeploymentBundle


## What next? Bash!

So after all of this, I decided that the best way for me to get a grasp of
what needs to be done for a solid, safe and (hopefully) simple deployment of Symfony2
project(s), was to dive in and write my own Bash script. This turned out to be a great
solution and has helped me understand quite a bit of what's going on behind-the-scenes.

That said, I'm no Linux/Bash guru! Feel free to improve any of these scripts, and send
a pull request :)



## My Deploy Goal

I just wanted to be able to call a simple script from the command line and have it handle
all the things needed to sync to a server and sort out any specific Symfony2 requirements
for updating at that end.

This is what I was aiming for:

    cd ~/path/to/project
    ./bin/deploy

sit back for a few seconds, take a sip of coffee and voilà my Symfony2 project
happily purring away on the destination server, with caches cleared, permissions updated, databases
migrated and so on!

__and my current solution looks like this__:

    cd ~/path/to/project
    ./bin/deploy dev|stage|live

Where the deploy live will only run if my local git repository is on the master branch.


## How to Use the Scripts

The idea is to provide a super simple bash script to start from. This should do the absolute
minimum to let you see that it's working properly, before adding more layers of functionality/complexity
to it.

__Prequisites__:
+ Your local Symfony2 project you will be deploying from is on Linux (Windows/Mac users should use something like VirtualBox)
+ you have rsync installed on this


#### Simple

+ [Deploy1](tree/master/bin/simple)  
    Super simple script to use as a starting point and to be sure your local
    development Symfony2 project is set up correctly.