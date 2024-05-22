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
PS：要求openssl加解密版本一致

## 5. vbox设置共享文件——Linux mount篇
```shell
$ sudo mount -t vboxsf <share> <mount_point>
$ sudo adduser $USER vboxsf
```

## 6. 使用tcpdump结合过滤条件提取pcap新文件
```shell
tcpdump tcp -ttttnnr old.pcap  -vvv port 443 -w part.pcap # 将old.pcap tcp端口包含443的packet保存到part.pcap
```

## 7. Ubuntu20.04 DNS修复
高版本的Ubuntu使用`systemd-resolved`管理DNS
### 查询状态
```shell
$ systemd-resolve --status
Global
       LLMNR setting: no                  
MulticastDNS setting: no                  
  DNSOverTLS setting: no                  
      DNSSEC setting: no                  
    DNSSEC supported: no                  
  Current DNS Server: 114.114.114.114     
         DNS Servers: 114.114.114.114     
                      114.114.115.115     
                      8.8.8.8             
Fallback DNS Servers: 8.8.4.4             
          DNSSEC NTA: 10.in-addr.arpa     
                      16.172.in-addr.arpa 
                      168.192.in-addr.arpa
                      17.172.in-addr.arpa 
                      18.172.in-addr.arpa 
                      19.172.in-addr.arpa 
                      20.172.in-addr.arpa 
                      21.172.in-addr.arpa 
                      22.172.in-addr.arpa 
                      23.172.in-addr.arpa 
                      24.172.in-addr.arpa 
                      25.172.in-addr.arpa 
                      26.172.in-addr.arpa 
                      27.172.in-addr.arpa 
                      28.172.in-addr.arpa 
                      29.172.in-addr.arpa 
                      30.172.in-addr.arpa 
                      31.172.in-addr.arpa 
                      corp                
                      d.f.ip6.arpa        
                      home                
                      internal            
                      intranet            
                      lan                 
                      local               
                      private             
                      test                

Link 3 (enp0s17)
      Current Scopes: DNS             
DefaultRoute setting: yes             
       LLMNR setting: yes             
MulticastDNS setting: no              
  DNSOverTLS setting: no              
      DNSSEC setting: no              
    DNSSEC supported: no              
  Current DNS Server: 114.114.114.114 
         DNS Servers: 114.114.114.114 
          DNS Domain: yourdomain.local

Link 2 (enp0s8)
      Current Scopes: none
DefaultRoute setting: no  
       LLMNR setting: yes 
MulticastDNS setting: no  
  DNSOverTLS setting: no  
      DNSSEC setting: no  
    DNSSEC supported: no
```
## 域名解析
```shell
$ systemd-resolve baidu.com 
baidu.com: 39.156.66.10                        -- link: enp0s17
           110.242.68.66                       -- link: enp0s17

-- Information acquired via protocol DNS in 28.4ms.
-- Data is authenticated: no
```
## 更新具体网口的DNS
```shell
$ sudo systemd-resolve --interface enp0s17 --set-dns 114.114.114.114 --set-domain yourdomain.local
```

## 选择时区并同步到北京时间
```shell
$ tzselect
$ sudo ntpdate  cn.pool.ntp.org
```
