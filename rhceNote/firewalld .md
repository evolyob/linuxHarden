```php
iptable告訴net_filter規則交互或丟棄
# 加22port 
iptable -A  INPUT -s 192.168.0.0/24 -p tcp --dport 22 -j ACCEPT

# 增加拒絕10.10.0.0/24用22 port
iptable -A  INPUT -s 10.10.0.0/24 -p tcp --dport 22 -j REJECT
# 刪除拒絕10.10.0.0/24用22 port
iptable -D  INPUT -s 10.10.0.0/24 -p tcp --dport 22 -j REJECT

# iptable默認規則 不允許
iptable -P INPUT DROP     //默認不讓進入，設定就無法遠端 ^^
iptable -P FORWARD DROP   //默認不允許轉發，不做控制
iptable -P OUTPUT ACCEPT  //默認不可出去，不做控制

白名單設定iptable
默認拒絕所有，只開放允許名單
iptable -A  INPUT -s <ip>/24 -p tcp --dport <> -j ACCEPT
iptable -A  INPUT -s <ip>/24 -p tcp --dport <> -j ACCEPT
iptable -P INPUT DROP


```
```php
iptable -L -t nat
Chain PREROUTING(policy ACCEPT)
target        port opt source       destination
DNAT         tcp   --  0.0.0.0/     0.0.0.0/0        tcp dpt:5000  192.168.0.1:5000
# 任何目的NAT訪問都會進去 192.168.0.1:5000

Chain INPUT(policy ACCEPT)
target        port opt source       destination
# 流量輸入ㄍ(可設黑白名單)
Chain OUTPUT(policy ACCEPT)
target        port opt source       destination
# 流量輸出(不另設定)
Chain FORWARD(policy ACCEPT)
target        port opt source       destination
# 流量轉發 (不另設定)

Chain POSTROUTING(policy ACCEPT)
target        port opt source       destination
MASQUERADE    all --  10.10.0.0/24   0.0.0.0/0                //ssh to wan
SNAT          all --  192.168.0.0/24 0.0.0.0/0 to:192.168.0.1 //storage to wan
# 能上網 來源的NAT 出去訪問上網
```

```php
firewalld 更簡單配置防火牆(幫轉換iptable指令)
firewalld-cmd --list-all

增加服務
firewalld-cmd --add-service=ftp
firewalld-cmd --list-services
移除服務
firewalld-cmd --remove-service=ftp
firewalld-cmd --list-services
```
```php
搭建web server
yum install httpd
echo firewall-test >> /var/www/html/index.html
systemctl restart httpd
systemctl enable httpd
curl <ip>

```
```
firewalld rich rule
firewalld-cmd --add-rich-rule="rule family=ipv4 source address=2.2.2.0/24 port=8089 protocol=tcp reject"

變成永久規則
firewalld-cmd --runtime-to-permanent
確認規則是否永久  
firewalld-cmd --reload
```
