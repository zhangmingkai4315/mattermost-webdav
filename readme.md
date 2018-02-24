# mattermost-webdav

```mattermost-webdav``` 用来存储grafana产生的静态文件，并提供mattermost消息进行使用，也可以作为通用的文件服务器进行使用

通用的配置如下：

```yaml
scope: /path/to/files
address: 0.0.0.0
port: 8080
getWithAuth: false
users:
  - username: admin
    password: admin
  - username: basic
    password: basic
    modify:   false
    rules:
      - regex: false
      - allow: false
      - path: /some/file
```

### 附curl测试方式

> 创建文件

```
curl -i -u admin:admin -T './config.ymal' http://localhost:8080/              
HTTP/1.1 100 Continue

HTTP/1.1 201 Created
Etag: "15164693d23b860df9"
Www-Authenticate: Basic realm="Restricted"
Date: Sat, 24 Feb 2018 13:38:44 GMT
Content-Length: 7
Content-Type: text/plain; charset=utf-8

Created
```

> 删除文件

```
curl -i -u admin:admin -X DELETE 'http://localhost:8080/config.ymal' 
HTTP/1.1 204 No Content
Www-Authenticate: Basic realm="Restricted"
Date: Sat, 24 Feb 2018 13:46:44 GMT
```

> 创建文件夹

```
curl -i -u admin:admin -X MKCOL 'http://localhost:8080/test' 
HTTP/1.1 201 Created
Www-Authenticate: Basic realm="Restricted"
Date: Sat, 24 Feb 2018 13:47:27 GMT
Content-Length: 7
Content-Type: text/plain; charset=utf-8

Created
```

