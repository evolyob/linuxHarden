```php
ls -Z  當前目錄的安全上下文的狀態
semanage
semanage port -l 端口安全上下文 使用哪個的tag標記
semanage port -a -t <PORT TYPE> -p tcp <no.>

semanage boolean -l | grep <>
semanage -P <> off

```
