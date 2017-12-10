# CDStore: Toward Reliable, Secure, and Cost-Efficient Cloud Storage via Convergent Dispersal
   
## Introduction
CDStore builds on an augmented secret sharing scheme called convergent dispersal, which supports deduplication by using deterministic content-derived hashes as inputs to secret sharing. It combines convergent dispersal with two-stage deduplication to achieve both bandwidth and storage savings and be robust against side-channel attacks. 


## Dependencies
CDStore is built on Ubuntu 12.04.3 LTS with gcc version 4.6.3. This software requires the following libraries:

 * OpenSSL (https://www.openssl.org/source/openssl-1.0.2a.tar.gz)
 * GF-Complete (https://github.com/ceph/gf-complete/archive/master.zip)
 * boost C++ library (http://sourceforge.net/projects/boost/files/boost/1.58.0/boost_1_58_0.tar.gz)
 * Leveldb (https://github.com/google/leveldb/archive/master.zip)

GF-Complete and Leveldb have been packed in `client/lib/` and `server/lib/` respectively.

## Installation

Install OpenSSL, Boost C++ library and snappy (that is necessary for Leveldb) by the following command:

```
$ sudo apt-get install libssl1.0.0 libboost-all-dev libsnappy-dev
```

Type the following commands to compile GF_Complete in `client/lib/gf_complete`:

```
$ cd client/lib/gf_complete
$ ./configure
$ make 
$ sudo make install
```

## Configurations

After installing the necessary libraries, following the instructions to config CDStore server and client.  

### Server

CDStore requires at least 4 servers for reliability. Thus, you need to configure at least 4 servers and `make` them, respectively. In a successfully configured server, it has a directory `server/meta/` which stores the deduplication index, file recipes and share containers. 

After a successful `make`, you will get the server program `SERVER`. Then, start it by the following command, where `[port]` is the port that CDStore server serves in.  

```
$ ./SERVER [port]
```

### Client

Modify the configuration file `client/config` to specify the server information. For example, if you have run 4 servers with `./SERVER [port]` on machines: 

```
192.168.0.30 with port 11030
192.168.0.31 with port 11031
192.168.0.32 with port 11032
192.168.0.33 with port 11033
```

You need to change `client/config` to:

```
192.168.0.30:11030
192.168.0.31:11031
192.168.0.32:11032
192.168.0.33:11033
```

Optionally, you can make advanced configure by modifying the total number of servers (4 by default), fault tolerance degree (1 by default), and security degree (0 by default) in `client/config`.

After all configurations, type `make` in `client/` to create client program `CLIENT`.  

### Quick Start

We provide scripts `auto_config.sh` and `auto_clean.sh` for quick configurations. You can run `./auto_config.sh` to compile and configure 4 servers, and run `./auto_clean.sh` to clean all temp outputs. 



## Usage

=== done here


 * After successful make

	usage: ./CLIENT [filename] [userID] [action] [secutiyType]

	- [filename]: full path of the file;
	- [userID]: user ID of current client;
	- [action]: [-u] upload; [-d] download;
	- [securityType]: [HIGH] AES-256 & SHA-256; [LOW] AES-128 & SHA-1


 * To upload a file "test", assuming from user "0" using AES-256 & SHA-256

	./CLIENT test 0 -u HIGH

 * To download a file "test", assuming from user "1" using AES-128 & SHA-1

	./CLIENT test 1 -d LOW



# MAINTAINER


 * Current maintainer

	- Yanjing Ren, UESTC, tinoryj@gmail.com
	- JinGang Ma, UESTC, demon64523@gmail.com

 * Original maintainer

	- Chuan QIN, the Chinese University of Hong Kong, chintran27@gmail.com

	- Mingqiang Li, Lenovo Hong Kong, mingqianglicn@gmail.com




# 临时测试脚本

> 正式版本删除

使用`AutoTest.sh`完成client、server编译并复制生成server2、server3、server4文件夹，便于测试
使用`AutoClean.sh`完成清理（删除复制生成的其他三个server文件夹、完成make clean）
