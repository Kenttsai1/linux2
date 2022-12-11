# 12/05

## 架設Server前 查看安全機制之常用指令

getenforce
```
Disable
```
cat /etc/selinux/config

```
SELLINUX=disable
```
systemctl status firewalld
```
查看防火牆狀況
```
## 安裝httpd

查詢是否安裝httpd
```
rpm -qa | grep httpd
```
## 實際操作

1. cd /var/www/html
pwd
ls

2. cd conf
ls
3. vim httpd.conf 修改
修改後重啟
4. systemctl restart httpd
查看狀態
5. systemctl status httpd
6. cat /run/httpd.pid
7. netstat -tunlp | grep 80

![](https://github.com/Kenttsai1/linux2/blob/main/LINUXPIC/1205-1.png)
![](https://github.com/Kenttsai1/linux2/blob/main/LINUXPIC/1205-12.png)
![](https://github.com/Kenttsai1/linux2/blob/main/LINUXPIC/1205-2.png)
![](https://github.com/Kenttsai1/linux2/blob/main/LINUXPIC/1205-3.png)

