## 1. vim 替换操作 &符号的作用 

## 2.  Linx sar 显示网速
```shell
sar -n DEV 1 60 
高版本sar可以指定网卡，例如--iface=enp0s8
```
## 3.数字证书的原理是什么？


## 4.使用openssl加密文件
```shell
# 加密
openssl <aes-256-cbc|others> -salt -pbkdf2 -a -e -in plaintext.txt -out encrypted.txt
# 解密
openssl <aes-256-cbc|others> -salt -pbkdf2 -a -d -in encrypted.txt -out decrypted.txt
# 选项说明：更多选项使用 openssl aes-256-cbc --help 查看
aes-256-cbc         算法为AES256，模式为CBC
-pbkdf2             Use password-based key derivation function 2
-salt               Use salt in the KDF (default)
-a                  Base64 encode/decode, depending on encryption flag
-e                  Encrypt
-d                  Decrypt
```

## 5. vbox设置共享文件——Linux mount篇
```shell
$ mount -t vboxsf <share> <mount_point>
```

## 6. 使用tcpdump结合过滤条件提取pcap新文件
```shell
tcpdump tcp -ttttnnr old.pcap  -vvv port 443 -w part.pcap # 将old.pcap tcp端口包含443的packet保存到part.pcap
```