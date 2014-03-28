## Setting up nvm.sh

[nvm.sh](https://raw.githubusercontent.com/creationix/nvm/master/nvm.sh) is a script, which can be used to manage Node.js installations. It can be found on github.

In order to install the script, please create some directory (within your home dir), and simple download the script using wget (or something similar). Then, source the script:

    $ . nvm.sh

Now, you should be able to download and install the latest version of Node.js (older versions should be also available):

    $ nvm install 0.10

## Using nvm.sh

Whenever you want to use a Node.js version installed with nvm.sh, simply go to the directory, where you've downloaded the nvm.sh script, source it:

    $ . nvm.sh

and tell it to use the installed Node.js version:

    $ nvm use 0.10


