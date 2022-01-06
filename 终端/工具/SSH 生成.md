

ssh-keygen -t rsa -C "注释"
* -t rsa 指定加密算法
* -C 注释


ssh-copy-id <目标服务器>  传输公钥到指定服务器
例如 `ssh-copy-id 192.168.1.2` 


ssh-keygen -R 106.14.161.138 移除 .ssh/konw_hosts 中缓存的ip
