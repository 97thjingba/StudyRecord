## http 代理

npm 原生支持 http 代理，直接设置即可

```
# 假设本地代理端口为8080  
npm config set proxy "http://localhost:8080"  
npm config set https-proxy "http://localhost:8080"  
  
# 有用户密码的代理  
npm config set proxy "http://username:password@localhost:8080"  
npm confit set https-proxy "http://username:password@localhost:8080"
```

# 假设本地代理端口为8080  
npm config set proxy "http://localhost:8080"  
npm config set https-proxy "http://localhost:8080"  
  
# 有用户密码的代理  
npm config set proxy "http://username:password@localhost:8080"  
npm confit set https-proxy "http://username:password@localhost:8080"  

## socks5 代理

npm 不支持 socks 代理，但是我们可以用一个工具将 http 代理转成 socks 代理，然后将 npm 代理地址设置到这个工具的地址。

```
# 假设本地socks5代理端口为8081  
# 首先安装转换工具  
npm install -g http-proxy-to-socks  
# 然后使用这个工具监听8080端口,支持http代理，然后所有8080的http代理数据都将转换成socks的代理数据发送到8081上  
hpts -s localhost:8081 -p 8080  
# 最后设置npm代理为8080  
npm config set proxy "http://localhost:8080"  
npm config set https-proxy "http://localhost:8080"
```

#### 假设本地socks5代理端口为8081  
#### 首先安装转换工具  
```npm install -g http-proxy-to-socks  ```
#### 然后使用这个工具监听8080端口,支持http代理，然后所有8080的http代理数据都将转换成socks的代理数据发送到8081上  
```hpts -s localhost:8081 -p 8080  ```
##### 最后设置npm代理为8080  
```js
npm config set proxy "http://localhost:8080"  
npm config set https-proxy "http://localhost:8080"  
```
相当于又加了一个中间层，将 http 转成 socks。

#### 删除代理

```js
npm config delete proxy  
npm config delete https-proxy
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTExNDQyODM1MDBdfQ==
-->