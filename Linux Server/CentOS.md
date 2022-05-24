

### 查看系统版本

```
cat /etc/centos-release
```

### 查看 CPU 信息

```
lscpu
```

参考： [How to check how many CPUs are there in Linux system](https://www.cyberciti.biz/faq/check-how-many-cpus-are-there-in-linux-system/)

### 修改 hostname

```
hostnamectl set-hostname --pretty LYH_Lab

hostnamectl set-hostname --transient LYH_Lab
```


### 修改用户名

```
usermod --login new_username --move-home --home path_to_the_new_home_dir old_username
```

## 参考

- [How can I rename an unix user?](https://serverfault.com/a/437343)
- [Linux sysadmin basics: User account management](https://www.redhat.com/sysadmin/linux-user-account-management)
- [7 ways to set your hostname in Fedora, CentOS, or Red Hat Enterprise Linux](https://www.redhat.com/sysadmin/set-hostname-linux)