# Deploy1

## Getting Started

A first super simple script -- it should help if you have any issues with other
things not working correctly.

All it's doing is setting up your local 'prod' environment.

__Use__:

    cd /path/to/your/project/bin/simple
    ./deploy1

This script runs a function to prepare your local project for deployment to a
different server. The __prep()__ function just does a basic Symfony2 clear cache and dumping
of assetic assets in the 'prod' environment. (if youre not using assetic, then just comment that line out).


_Sample output from Deploy1_:

[![Deploy1 output](https://github.com/ZermattChris/Symfony2-SimpleDeployScripts/raw/master/bin/deploy1/deploy1-output.jpg)](https://github.com/ZermattChris/Symfony2-SimpleDeployScripts/raw/master/bin/deploy1/deploy1-output.jpg)

