# Mr.2

[![Build Status](https://travis-ci.org/txthinking/mr2.svg?branch=master)](https://travis-ci.org/txthinking/mr2) [![License: GPL v3](https://img.shields.io/badge/License-GPL%20v3-blue.svg)](http://www.gnu.org/licenses/gpl-3.0)
[![EN](https://img.shields.io/badge/English-README-blue.svg)](https://github.com/txthinking/mr2/blob/master/README.md)

### Table of Contents

* [Mr.2是什么](#mr2是什么)
* [下载](#下载)
* [**服务端**](#服务端)
* [**客户端**](#客户端)
* [贡献](#贡献)
* [协议](#协议)

## Mr.2是什么

Mr.2 可以帮助你将内网服务器暴露在外网. 支持 TCP/UDP 协议, 当然也支持HTTP协议.<br/>
让这个世界简单点.

## 下载

| 下载 | 系统 | 架构 |
| --- | --- | --- |
| [mr2](https://github.com/txthinking/mr2/releases/download/v20190519/mr2) | Linux | amd64 |
| [mr2_darwin_amd64](https://github.com/txthinking/mr2/releases/download/v20190519/mr2_darwin_amd64) | MacOS | amd64 |
| [mr2_windows_amd64.exe](https://github.com/txthinking/mr2/releases/download/v20190519/mr2_windows_amd64.exe) | Windows | amd64 |

更多平台下载请查看 [releases](https://github.com/txthinking/mr2/releases). 或`go get github.com/txthinking/mr2/cli/mr2`.

### 服务端

```
$ mr2 server -l :9999 -p password
```

```
# 只允许部分端口, 并针对每个端口设置密码
$ mr2 server -l :9999 -P '5678 password' -P '6789 password1'
```

### 客户端

```
# 将本地服务 127.0.0.1:1234, 暴露在外网: server_address:5678
$ mr2 client -s server_address:port -p password -P 5678 -c 127.0.0.1:1234
```

```
# 将本地目录 /path/to/www, 以HTTP协议暴露在外网: server_address:5678
$ mr2 client -s server_address:port -p password -P 5678 --clientDirectory /path/to/www
```

### 示例

#### 访问内网HTTP服务

```
$ mr2 client -s server_address:port -p password -P 5678 -c 127.0.0.1:8080

# 然后
你的外网HTTP服务: server_address:5678
```

#### SSH登录到内网机器

```
$ mr2 client -s server_address:port -p password -P 5678 -c 127.0.0.1:22

# 然后
$ ssh -oPort=5678 user@server_address
```

#### 访问内网DNS服务

```
$ mr2 client -s server_address:port -p password -P 5678 -c 127.0.0.1:53

# 然后
你的外网DNS服务: server_address:5678

$ dig github.com @server_address -p 5678
```

#### 通过HTTP访问内网机器上的文件

```
$ mr2 client -s server_address:port -p password -P 5678 --clientDirectory /path/to/www

# 然后
你的外网HTTP服务: server_address:5678
```

#### 任何基于TCP/UDP的你能想到的想法

...


## 贡献

请先阅读 [CONTRIBUTING.md](https://github.com/txthinking/mr2/blob/master/.github/CONTRIBUTING.md)

## 协议

以 GPLv3 协议开源
