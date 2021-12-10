### vue-element-admin配置gz压缩以及nginx配置gz

#### vue项目配置:

* 首先安装`compression-webpack-plugin`

  * `npm install compression-webpack-plugin@6.1.1 `
  * 版本高于6.1.1会报undefind错误

* 配置vue.config.js文件

  * ```js
    // ....
    config
          .when(process.env.NODE_ENV !== 'development',
            config => {
        // 以下是新增内容
        		config
                	.plugin('CompressionPlugin')
                	.use('compression-webpack-plugin', [{
                  		test: /\.js$|\.css$|\.html$/, // gzip压缩规则
                  		threshold: 10240, // 大于10K的数据会被压缩
                  		algorithm: 'gzip', // 压缩方式
                  		minRatio: 0.8 // 压缩比小于这个的才压缩
                	}])
                	.end()
        //.....
    ```

  * 执行打包命令:  npm run build:prop (官方文档里的打包命令)

* 生成dist目录下可以看到.gz文件

  * ![image-20211210150348200](https://cdn.jsdelivr.net/gh/wzc520pyfm/Picbed_PicGo@master/img/image-20211210150348200.png)

### nginx配置

将dist文件是上传到服务器, 然后在nginx的config文件里的http下添加如下配置

* ```config
  gzip on;
  
      gzip_static on;
  
      gzip_buffers 4 16k;
  gzip_comp_level 5;
      
  gzip_types text/plain application/javascript application/x-javascript text/css application/xml text/javascript application/x-httpd-php image/jpeg image/gif image/png;
  ```

* 或在server下添加:

* ```config
  gzip on;
      
  	gzip_min_length 1k;
      
  	gzip_comp_level 9;
      
  	gzip_types text/plain application/javascript application/x-javascript text/css application/xml text/javascript application/x-httpd-php image/jpeg image/gif image/png;
      
  	gzip_vary on;
      
  	# 配置禁用 gzip 条件，支持正则，此处表示 ie6 及以下不启用 gzip（因为ie低版本不支持）
      
  	gzip_disable "MSIE [1-6]\.";
  ```

* nginx部署vue项目的写法如下: 

* ```config
  server {
          listen       3333;
          server_name  localhost;
  	# compression-webpack-plugin 配置
      
  	gzip on;
      
  	gzip_min_length 1k;
      
  	gzip_comp_level 9;
      
  	gzip_types text/plain application/javascript application/x-javascript text/css application/xml text/javascript application/x-httpd-php image/jpeg image/gif image/png;
      
  	gzip_vary on;
      
  	# 配置禁用 gzip 条件，支持正则，此处表示 ie6 及以下不启用 gzip（因为ie低版本不支持）
      
  	gzip_disable "MSIE [1-6]\.";
  
          #charset koi8-r;
  
          #access_log  logs/host.access.log  main;
  
          location / {
              root  C:\Users\Administrator\Desktop\vue-project\watch\dist;
  	    try_files $uri $uri/ @router;
              index  index.html index.htm;
          }
  	location /api {
                          #网站静态资源路径。此路径仅供参考，具体请您按照实际目录操作。
                          proxy_pass http://xxx.xx.xx.xxx:xxxx;
                          proxy_connect_timeout 600;
                          proxy_read_timeout 600;
          }
  
  	location @router {
  	    rewrite ^.*$ /index.html last;
  	}
  
      }
  ```

* nginx启动命令: start nginx

### 启动后可以看到浏览器请求的资源包明显减小

