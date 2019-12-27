# 2x2coin


https://2x2coin.space     Official Website
http://2x2block.space     ( Blockexplorer including API )

Windows wallet https://github.com/2X2coin/2x2coin/raw/master/release/2X2-qt.exe


How to compile the Linux Deamon , tested and working on ubtunu 14 - 16.04 and 17.  version . 16.04 is recommended

Set up a swapfile if your system has less than 1.5GB of memory:


fallocate -l 2G /swapfile

chown root:root /swapfile

chmod 0600 /swapfile

sudo bash -c "echo 'vm.swappiness = 10' >> /etc/sysctl.conf"

mkswap /swapfile

swapon /swapfile


If fallocate doesn’t work, you can use dd if=/dev/zero of=/swapfile bs=1024 count=1024288 instead.

Initialize swapfile automatically on boot

echo '/swapfile none swap sw 0 0' >> /etc/fstab

Install all required dependencies:

apt-get update && apt-get upgrade
apt-get install nano ntp unzip git build-essential libssl-dev libdb-dev libdb++-dev libboost-all-dev libqrencode-dev aptitude && aptitude install miniupnpc libminiupnpc-dev

Pull the source code from github, or upload it yourself:

git clone https://github.com/2X2coin/2x2coin.git

now you compile the leveldb:

cd 2x2coin/src/leveldb

chmod +x build_detect_platform

make clean

make libleveldb.a libmemenv.a

Return to source directory, and compile the daemon:

cd ..

make -f makefile.unix

Strip the file to make it smaller, then relocate it:

strip 2X2d

cp 2X2d /usr/bin

Now run the daemon:

2X2d

It will return an error, telling you to set up config file in a directory. Now we’ll set up the config file. Note that this is case sensitive.

nano ~/.2X2/2X2.conf

Add the following, save and exit:

daemon=1

server=1

rpcuser=(username)

rpcpassword=(strong password)

Run 2X2d once more and if you did everything correctly, your daemon is now online! Type YOURCOINd help for a full list of commands available.
