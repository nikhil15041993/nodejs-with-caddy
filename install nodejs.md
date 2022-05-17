## Removing Nodejs and Npm

```
sudo apt-get remove nodejs npm node
sudo apt-get purge nodejs
```

Now remove .node and .npm folders from your system


```
sudo rm -rf /usr/local/bin/npm 
sudo rm -rf /usr/local/share/man/man1/node* 
sudo rm -rf /usr/local/lib/dtrace/node.d 
sudo rm -rf ~/.npm 
sudo rm -rf ~/.node-gyp 
sudo rm -rf /opt/local/bin/node 
sudo rm -rf opt/local/include/node 
sudo rm -rf /opt/local/lib/node_modules  

sudo rm -rf /usr/local/lib/node*
sudo rm -rf /usr/local/include/node*
sudo rm -rf /usr/local/bin/node*
```

Go to home directory and remove any node or node_modules directory, if exists.

You can verify your uninstallation by these commands; they should not output anything.

```
which node
which nodejs
which npm
```

## Installing NVM (Node Version Manager) by downloading and running a script


```
curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.34.0/install.sh | bash
```

The command above will clone the NVM repository from Github to the ~/.nvm directory:

Close and reopen your terminal to start using nvm or run the following to use it now:

```
export NVM_DIR="$HOME/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"  # This loads nvm
[ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion"  # This loads nvm bash_completion
```
As the output above says, you should either close and reopen the terminal or run the commands to add the path to nvm script to the current shell session. You can do whatever is easier for you.

Once the script is in your PATH, verify that nvm was properly installed by typing:

```
nvm --version
```
which should give this output:
```
0.34.0
```
Installing Node.js and npm

```
nvm install node
nvm install --lts
sudo apt install nodejs
```

Once the installation is completed, verify it by printing the Node.js version:

```
node --version
```

should give this output:

```
v12.8.1
```

Npm should also be installed with node, verify it using

```
npm -v
```
should give:
```
6.13.4
```
Extra - [Optional] You can also use two different versions of node using nvm easily

nvm install 8.10.0 # just put the node version number Now switch between node versions

```
$ nvm ls
->     v12.14.1
        v13.7.0
default -> lts/* (-> v12.14.1)
node -> stable (-> v13.7.0) (default)
stable -> 13.7 (-> v13.7.0) (default)
iojs -> N/A (default)
unstable -> N/A (default)
lts/* -> lts/erbium (-> v12.14.1)
lts/argon -> v4.9.1 (-> N/A)
lts/boron -> v6.17.1 (-> N/A)
lts/carbon -> v8.17.0 (-> N/A)
lts/dubnium -> v10.18.1 (-> N/A)
In my case v12.14.1 and v13.7.0 both are installed, to switch I have to just use

```
```
nvm use 12.14.1
```
Configuring npm for global installations In your home directory, create a directory for global installations:

```
mkdir ~/.npm-global
```
Configure npm to use the new directory path:

```
npm config set prefix '~/.npm-global'
```
In your preferred text editor, open or create a ~/.profile file if does not exist and add this line:

```
PATH="$HOME/.npm-global/bin:$PATH"
```

On the command line, update your system variables:

```
source ~/.profile
```

That's all
