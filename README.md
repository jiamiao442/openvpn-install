
## openvpn-install
OpenVPN [road warrior](http://en.wikipedia.org/wiki/Road_warrior_%28computing%29) installer for Ubuntu, Debian, AlmaLinux, Rocky Linux, CentOS and Fedora.

This script will let you set up your own VPN server in no more than a minute, even if you haven't used OpenVPN before. It has been designed to be as unobtrusive and universal as possible.

### Installation 1
Run the script and follow the assistant:

```
# 建议关闭selinux

setenforce 0
sed -i  's/SELINUX=enforcing/SELINUX=disabled/' /etc/selinux/config 

# 安装openvpn
cd /opt
&& wget https://www.ghproxy.cn/https://raw.githubusercontent.com/jiamiao442/openvpn-install/master/openvpn-install.sh -O openvpn-install.sh \
&& bash openvpn-install.sh
```

Once it ends, you can run it again to add more users, remove some of them or even completely uninstall OpenVPN.

### Installation 2
一键安装openvpn with google auth
已在rockylinux 9 测试。

```
# 建议更新系统，防止报错。 
dnf update

# 建议关闭selinux

setenforce 0
sed -i  's/SELINUX=enforcing/SELINUX=disabled/' /etc/selinux/config 

# 安装openvpn
cd /opt
&& wget https://www.ghproxy.cn/https://raw.githubusercontent.com/jiamiao442/openvpn-install/master/openvpn-with-google-auth-install.sh -O openvpn-with-google-auth-install.sh \
&& bash openvpn-with-google-auth-install.sh
```
用户默认密码：123456

### 遇见的问题
1. 验证失败。日志如下
```
PLUGIN AUTH-PAM: BACKGROUND: user 'test1' failed to authenticate: Authentication service cannot retrieve authentication info
192.168.174.1:65381 PLUGIN_CALL: POST /usr/lib64/openvpn/plugins/openvpn-plugin-auth-pam.so/PLUGIN_AUTH_USER_PASS_VERIFY status=1
192.168.174.1:65381 PLUGIN_CALL: plugin function PLUGIN_AUTH_USER_PASS_VERIFY failed with status 1: /usr/lib64/openvpn/plugins/openvpn-plugin-auth-pam.so
192.168.174.1:65381 TLS Auth Error: Auth Username/Password verification failed for peer
```
解决问题：关闭selinux
```
setenforce 0
sed -i  's/SELINUX=enforcing/SELINUX=disabled/' /etc/selinux/config 
```