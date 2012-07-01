# Symfony2 Simple Deploy Scripts

[![Deploy1 output](https://github.com/ZermattChris/Symfony2-SimpleDeployScripts/raw/master/img/deploy-concept.jpg)](https://github.com/ZermattChris/Symfony2-SimpleDeployScripts/raw/master/bin/img/deploy-concept.jpg)


## Background


**Disclaimer**: _I'm still learning both Symfony2 and how best to deploy, so please let me know if you find a mistake or
a missing step or two_ :-)

Getting started with Symfony2 can be a daunting task for those of us new to it and one of the areas that
I found the most confusing, was how to properly deploy a project to various servers.

_Should I be using_:

+ Capifony?
+ git push/pull to remote?
+ Some pre-built Deploy Bundle?
+ rsync?
+ ssh?

Although project deployment is a critical & fundamental part of any Symfony2 project, there didn't
seem to be any consensus as how best to go about this. As I couldn't find any _gentle_ introduction to the
subject, I have put this together in the hopes that some of the existing Symfony2 gurus out there
will point out where I'm making mistakes or missing things.


__Tip__:
If you're doing your development work in Windows and want to build Symfony2 based projects, do yourself
a huge favour and install VirtualBox (or similar) and put your project on a Linux of your choice. It makes
everything smoother (well, once you've learned how to build/maintain a LAMP server...)


### Capifony
I found Capifony to be interesting, but rather opaque (not a lot of docs and even after I got it all working,
was still not quite sure how to use it). I also don't know Ruby and the thought of having
to dig through yet-another-language to be able to follow along didn't appeal greatly (plus I found Ruby a
royal pain to install properly).

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
I quickly discovered that most are just wrappers around rsync and ssh. Inevitably getting
a solid deploy concept working means having to tweak things for your specific needs -- having the
various linux commands burried in a Symfony2 php bundle just made it more difficult to understand and
modify.

+ http://knpbundles.com/aerialls/MadalynnPlumBundle
+ http://knpbundles.com/dator/DeployBundle
+ https://github.com/BeSimple/BeSimpleDeploymentBundle


## What next? Bash!

So after all of this, I decided that the best way to get a grasp of how to build a solid, safe and
(hopefully) simple deployment of Symfony2 project(s), was to dive in and write my own Bash script.
This turned out to be a great solution and has helped me understand quite a bit of what's going
on behind-the-scenes.

That said, I'm no Linux/Bash guru!
Feel free to improve any of these scripts (send a pull request) or to point out where I've missed something important.

+ [Writing Shell Scripts](http://linuxcommand.org/wss0010.php)
+ [Bash Function Examples](http://www.thegeekstuff.com/2010/04/unix-bash-function-examples/)


## The Deploy Goal

To just call a simple script from the command line and have it handle all the things needed to sync to a
server and sort out any specific Symfony2 requirements for updating at that end.

This is what I was aiming for:

    cd ~/path/to/project
    ./bin/deploy

then sit back for a few seconds, take a sip of coffee and voilà!, a Symfony2 project
happily purring away on the destination server, with caches cleared, permissions updated, databases
migrated and so on!

__my final working solution looks like this__:

    cd ~/path/to/project
    ./bin/deploy dev|stage|fix|live

Where the deploy _live_ option will only run if my local git repository is on the master branch, to keep
from mistakenly deploying a development or feature branch to the live production server.


## How to Use the Scripts

The scripts are meant as starting points for your own deploys. Each does the absolute
minimum required to let you see that it's working properly, before adding more layers of
functionality/complexity.

__Prequisites__:
+ Your local Symfony2 project you will be deploying from is on Linux (Windows/Mac users should
use something like VirtualBox)
+ you have rsync installed on your servers (check in the console with **rsync --version**)


#### Scripts

+ [Deploy1](Symfony2-SimpleDeployScripts/tree/master/bin/deploy1/) <br />
    Super simple script to use as a starting point and to check that your local
    development Symfony2 project is set up correctly.