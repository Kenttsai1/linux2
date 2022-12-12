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
    ServerName example.com  |a.com b.com
    ServerAlias www.example.com |a.com b.com
    ServerAdmin webmaster@example.com |a.com b.com
    DocumentRoot /var/www/example.com/public_html |a.com b.com

    <Directory /var/www/example.com/public_html> |a.com b.com
        Options -Indexes +FollowSymLinks
        AllowOverride All
    </Directory>

    ErrorLog /var/log/httpd/example.com-error.log
    CustomLog /var/log/httpd/example.com-access.log combined
</VirtualHost>
```


到windows 更改hosts

![](https://i.imgur.com/YWFoumA.png)
![](https://i.imgur.com/ur7Glo6.png)

**OK**

![](https://i.imgur.com/PawjHf8.png)