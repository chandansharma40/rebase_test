# Installing nodes on Ubuntu Local Machine
## Pre-requisites
Make sure your local machine has Git and Git-LFS. Instructions are available [here](https://git-lfs.github.com/).
```
Example: using command line
First install curl(if not already installed). Followed by commands shown below
sudo apt-get install curl
curl -s https://packagecloud.io/install/repositories/github/git-lfs/script.deb.sh | sudo bash
sudo apt-get install git-lfs
git lfs install [output:Git LFS initialized] 
 
or

Example:Download git-lfs-2.3.0 from web then  
cd git-lfs-2.3.0  
./install.sh    [output:Git LFS initialized]  
git lfs install [output: Git LFS initialized]  
```
Now you need to get cmake-3.2.2, gcc-4.9 and g++-4.9 set-up in your local machine
1. Cmake
```
wget http://www.cmake.org/files/v3.2/cmake-3.2.2.tar.gz
tar xzvf cmake-3.2.2.tar.gz;
cd cmake-3.2.2;
./configure --prefix=/usr/local;
make && make install;
cd ..
rm -rf cmake-3.2.2
```
2. GCC-4.9 and G++-4.9
  ```
  sudo apt-get install gcc-4.9 g++4.9
  sudo ln -s /usr/bin/gcc-4.9 /usr/bin/gcc 
  sudo ln -s /usr/bin/g++-4.9 /usr/bin/g++ 
  ```

## Preparing the Folder Structure
1. Make a folder named `rxm` in your `/home` folder. Open terminal using <code>Ctrl + Alt + T</code>
```
mkdir rxm && cd rxm
```
2. Now we're ready to clone the repositories in your local machine
   In `/home/rxm`,
```
git init
git clone https://<username>:<password>@github.com/ReflexionMed/RxOne.git

```
3. In the same folder `/home/rxm`, we need to have RxMachineDependencies as well, so after cloning RxOne, in the same location
```
git init
git clone https://<username>:<password>@github.com/ReflexionMed/RxMachineDependencies.git
```
4. Also, run the following command from the same location
`mkdir rxdeps-native`
5. Now if you do `ls` you should be able to see three folders at the location `/home/rxm`

## Building RxMachineDependencies

Note that you must *not* source the QNX environment file to build natively.

You can perform all the below automatically by running

```shell
cd /path/to/RxMachineDependencies
./native-install.sh /path/to/prefix
```

Replace `/path/to/prefix` with `/home/rxm/rxdeps-native`

## Building the nodes
Go to `/home/rxm/RxOne/RxMachine` and run the following commands
```
./change_ip.sh 127.0.0.1
mkdir build && cd build
cmake -DCMAKE_PREFIX_PATH=<path-to-rxdeps-native> ..
```
This will generate all the build files for all the nodes in the folder `/RxMachine/build`
Now to build all the nodes at once you can run `make -j8` right away or goto a particular node and then do `make -j8`

Now in the folder `/RxMachine/build/<any-node>`, you'll find an executable which you can run using `./<executable>`

