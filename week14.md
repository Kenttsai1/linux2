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



## 模組設定
系統內使用者可以使用個人網頁
1. cd /etc/httpd/conf.d
 ls
2. vim userdir.conf  修改文件誠如片所示
![](https://github.com/Kenttsai1/linux2/blob/main/LINUXPIC/1205-21.png)
3. systemctl restart httpd 重啟

更換視窗到user@kk1 ~
4. mkdir public_html 建立資料夾
5. cd public_html/
ls
6. echo "hello world" > hi.htm 做一個hi.htm
7. systemctl restart httpd
8. 到瀏覽器 輸入192.168.56.108/~user/hi.htm
```
若出現Forbidden 則需要更改user權限
```
cd /home
ll 查看
9. chmod 755 user 更改權限能讀
到user裡面 ll查看 public_html權限是否有r,x
![](https://github.com/Kenttsai1/linux2/blob/main/LINUXPIC/1205-2.png)

## 在同根目錄中存取var/www/html外的mydata資料夾中的網頁
可以使用創造連結或Alias(虛擬目錄)實現
以下使用Alias 創造別名
1. cd /
2. mkdir mydata2
cd mydata2
3. echo "4567" > 2.htm
4. 到 conf下  vim httpd.conf 最下面添加
![](https://github.com/Kenttsai1/linux2/blob/main/LINUXPIC/1205-31.png)
5. 修改完重啟
6. systemctl restart httpd
7. 到瀏覽器 輸入192.168.56.108/mydata2/2.htm
![](https://github.com/Kenttsai1/linux2/blob/main/LINUXPIC/1205-3.png)

