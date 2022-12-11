## Ngrok

安裝時有些需在前方加./
安裝基本按照下面網址安裝

使用時若出現ngrok 502 bad gateway (可能是因為沒開啟httpd)
啟動(systemctl start httpd : running)
檢查tcp/udp有沒有開netstat -tunlp | grep 80 



## 參考來源
```
https://learn.markteaching.com/ngrok-webhook/
https://askie.today/ngrok-localhost-server-settings/
```