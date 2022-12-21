# 12/12

# 指令

pwd

cd /var/www
ls

mkdir a.com b.com
ls

cd a.com

echo "www.a.com" > index.html
cd..

cd b.com
echo "www.b.com" > index.html

cd /etc/httpd/conf.d



vim a.com.conf b.com.conf

```
<VirtualHost *:80>
    ServerName a.com
    ServerAlias www.a.com
    ServerAdmin webmaster@a.com
    DocumentRoot /var/www/a.com

    <Directory /var/www/a.com>
        Options -Indexes +FollowSymLinks
        AllowOverride All
    </Directory>

    ErrorLog /var/log/httpd/a.com-error.log
    CustomLog /var/log/httpd/a.com-access.log combined
</VirtualHost>
```

b.com.conf
```
<VirtualHost *:80>
    ServerName b.com
    ServerAlias www.b.com
    ServerAdmin webmaster@b.com
    DocumentRoot /var/www/b.com

    <Directory /var/www/b.com>
        Options -Indexes +FollowSymLinks
        AllowOverride All
    </Directory>

    ErrorLog /var/log/httpd/b.com-error.log
    CustomLog /var/log/httpd/b.com-access.log combined
</VirtualHost>
```


到windows 更改hosts

![](https://i.imgur.com/YWFoumA.png)
![](https://i.imgur.com/ur7Glo6.png)

**OK**

![](https://i.imgur.com/PawjHf8.png)


## 



加上 Options Indexes 瀏覽網頁後，可呈現檔案列表
，若沒有Options Indexes會找不到出現Forbidden

在 /var/www/a.com裡面放a~d.txt可查看

能看見自己資料夾本身的檔案

www.a.com/a/

![](https://i.imgur.com/pVaBNLn.png)

回到根目錄 cd /

建立mytmp 

echo "hi" > hi.txt

建完後回到 cd /var/www/a.com/a


## 做一個符號連結 ln -s /mytmp mytmp

![](https://i.imgur.com/q40fDDX.png)

修改a.com.conf 在/etc/httpd/conf.d

![](https://i.imgur.com/qHqOaLE.png)

**因為多了FollowSymLinks**
**能看見自己資料夾本身的檔案以及連結的資料夾**

```
但FollowSymLinks這個選項有安全性的問題，能不用就盡量不用
```

AllowOverride 允許推翻選項設定

# Access control 驗證帳號及密碼


先在a.com下建立 secure的資料夾
echo "important data" > data.txt

若他人知道連結便可直接看見data.txt，之後要做的是加密使其更加安全


1.  讓Apache允許目錄可使用自訂權限

    到/etc/httpd/conf.d
    
    vim a.com.conf修改成
    
    ![](https://i.imgur.com/Ujk5GJq.png)

    
2.  為使用者設定密碼

    回到 /var/www/a.com/secure
    
    設定密碼檔
    
    htpasswd -c .htpasswd tom  **-c只有第一次設定需要，之後設定mary就不需要-c**
    
    輸入兩次密碼
    
    編輯目錄驗證設定檔
    
    vim .htaccess
    
    添加
    
    ```
    AuthType Basic
    AuthName "Private File Area"
    AuthUserFile /var/www/a.com/secure/.htpasswd
    Require valid-user

    ```

    ![](https://i.imgur.com/isZwZ16.png)

    systemctl restart httpd

    www.a.com/secure/data.txt
    ![](https://i.imgur.com/aiTsl9m.png)
    
    
# FTP伺服器套件- vsftpd



檢查是否已安裝 ``rpm -qa | grep vsftpd `` 

安裝 ``yum install vsftpd`` 

FTP站台的根目錄 `` /var/ftp/ ``

之後使用 winscp **匿名登入**

若無法登入可能是ftp沒有開啟

檢查 `` netstat -tunlp | grep 21``

啟動 `` systemctl start vsftpd``

查看stauts ``systemctl status vsftpd``

再來便可以登入，也可看見pub的資料夾
可以下載但不能上傳

檢查pub的權限 ``ll `` 

因為我們是匿名登入沒有權限 因此更改有寫入的權限
**資料夾要注意切換出去**
``chmod 777 pub``
``chmod 777 ftp``

**資料夾沒問題了，再來是伺服器的問題**
cd /etc/vsftpd/
vim vsftpd.conf

![](https://i.imgur.com/fJKlToR.png)

**之後便可以匿名來上傳及下載**



