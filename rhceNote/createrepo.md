```php
rpm -ivh <安裝指定版本> 
rpm -evh <移除指定>
rpm -qpi 查詢未安裝的內容
rpm -qa | grep <> 查看安裝什麼
rpm -ql 安裝的路徑

```

```
要有rpm包和repodata才能搭建倉庫
path: /etc/yum.conf  配置文件
path: /etc/yum.repos.d  倉庫文件目錄

清空預設文件
[uke]
name = uke repo
enable = yes
gpgcheck = 0
baseurl = file:///<repo location> 代表本地系統的根

```
```
yum -y install yum-utils
yum-config-manager --add-repo=https://<url>
```
```
 局域庫建立
reposync --repo <syncRepoName> -p /<repoName>/

find ./ -name *.rpm -exec mv {} . \;
// rpm移動到當前目錄


yum install createrepo
createrepo -v  /<repoName>/
```
