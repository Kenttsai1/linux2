# Samba


### 安裝SAMBA
CentOS上安裝Samba
```
yum install samba samba-client samba-common -y

```

建立欲共享之目錄建立
mkdir 目錄

設定
安裝完成Samba後，samba的設定檔位置路徑為 /etc/samba/smb.conf，接著設定samba設定檔
```
vi /etc/samba/smb.conf
```
insert 加入[test]


testparm 測試


啟動SAMBA服務
```
systemctl start smb
```

更新密碼
```
smbpasswd -a user
user
```
可以到資料夾打\\IP位置進入
```
user
user
```
新稱檔案
```
echo "hi">a.txt
```






## 資料參考
```
https://josephjsf2.github.io/linux/2019/11/01/share_centos_folder_with_windows.html
```