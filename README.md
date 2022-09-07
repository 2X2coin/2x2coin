# 2x2coin-K1


https://2x2coin.space     Official Website
http://2x2block.space     ( Blockexplorer including API )

Windows wallet https://github.com/2X2coin/2x2coin/raw/master/release/2X2-qt.exe

## How to compile and use the Linux Deamon
Tested and working on Ubtunu 14 - 16.04 and 17.  Version 16.04 is recommended.
Versions 18.04 and later do not currently compile due to changes in OpenSSL 1.1
and the Boost C++ library in that version.

### Swapfile

You can check if your server has a swap file already with the ```swapon``` command.  If your system has less than 1.5GB of memory, you'll want at least a 2GB swap area.  Add a new swapfile with:
```
sudo fallocate -l 2G /swapfile
sudo chown root:root /swapfile
sudo chmod 0600 /swapfile
sudo bash -c "echo 'vm.swappiness = 10' >> /etc/sysctl.conf"
sudo mkswap /swapfile
sudo swapon /swapfile
```
If fallocate doesn’t work, you can instead use:
```
sudo dd if=/dev/zero of=/swapfile bs=1024 count=1024288
```
Initialize the swapfile to mount automatically on boot:
```
sudo echo '/swapfile none swap sw 0 0' >> /etc/fstab
```

### Install all required dependencies

```sudo apt-get update && sudo apt-get upgrade
sudo apt-get -y install nano ntp unzip git build-essential libssl-dev \ 
  libdb-dev libdb++-dev libboost-all-dev libqrencode-dev aptitude
sudo aptitude -y install miniupnpc libminiupnpc-dev
```
If you get an error mentioning lock files, you probably have a desktop or background package update tool running that prevents other apt changes from happening.  You can use the ```lsof``` utility to figure out what program holds the lock and then pause it from running.

Pull the source code from github, or download it yourself:
```
git clone https://github.com/2X2coin/2x2coin.git
```

### Compiling the software

Now you compile the included leveldb:
```
cd 2x2coin/src/leveldb
chmod +x build_detect_platform
make clean
make libleveldb.a libmemenv.a
```
Return to the source directory, and compile the daemon:
```
cd ..
make -f makefile.unix
```
Strip the file to make it smaller, then relocate it:
```
strip 2X2d
sudo cp 2X2d /usr/bin
```
Now run the daemon:
```
X2d
```
It should return an error, telling you to set up config file in a directory. 

## Create a config file

Now we’ll set up the config file. Note that this is case sensitive.
```
nano ~/.2X2/2X2.conf
```
Add the following, save and exit:
```
daemon=1
server=1
rpcuser=(username)
rpcpassword=(strong password)
```
Run 2X2d once more and if you did everything correctly, your daemon is now online! 
## Command summary
Type:
```
YOURCOINd help
```
for a full list of commands available.
