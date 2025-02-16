# sub-web

基于 vue-cli 与 [tindy2013/subconverter](https://github.com/tindy2013/subconverter) 后端实现的配置自动生成。

## Table of Contents

- [ChangeLog](#ChangeLog)
- [Docker](#Docker)
- [Requirements](#Requirements)
- [Install](#install)
- [Usage](#usage)
- [Related](#Related)
- [Contributing](#contributing)
- [License](#license)

## ChangeLog

- 20200730

  - 独立各类后端配置到 .env 文件中，现在修改后端只需要修改 .env 即可。


搭建Sub-Web前端
更新系统并安装 Node 与 Yarn
依次运行下面四行代码，若是 Debian/Ubuntu 系统，请自行替换下面前两行命令中的 yum 为 apt

yum update -y
yum install -y curl wget sudo nodejs git
npm install -g cnpm --registry=https://registry.npm.taobao.org
cnpm install -g yarn
命令执行完毕以后，请运行下面的代码查询 Node 与 Yarn 是否安装成功，若是成功会返回版本号，如下图。

node -v
yarn --version

下载并安装 Sub-Web
拉取 sub-web 程序，并进入 sub-web 文件夹

git clone https://github.com/CareyWang/sub-web.git
cd sub-web
在项目目录中安装构建依赖项，构建的过程稍微有点长

yarn install
使用 webpack 运行 Web 客户端以进行本地开发。

yarn serve
到目前为止，浏览器访问 http://服务器ip:8080/ 应该可以进行前端 sub-web 的预览了。
浏览器访问 <http://localhost:8080/>

## Deploy

发布到线上环境，你需要安装依赖，执行以下打包命令，生成的 dist 目录即为发布目录。如需修改默认后端，请修改 src/views/Subconverter.vue 中 **defaultBackend** 配置项。

```shell
yarn build
```

你需要安装 nginx (或其他 web 服务器)并正确配置。以下为示例配置，你需要修改 example.com 为自己域名并配置正确的项目根路径（https 自行配置）。

```shell
server {
    listen 80;
    server_name example.com;

    root /var/www/http/sub-web/dist;
    index index.html index.htm;

    error_page 404 /index.html;

    gzip on; #开启gzip压缩
    gzip_min_length 1k; #设置对数据启用压缩的最少字节数
    gzip_buffers 4 16k;
    gzip_http_version 1.0;
    gzip_comp_level 6; #设置数据的压缩等级,等级为1-9，压缩比从小到大
    gzip_types text/plain text/css text/javascript application/json application/javascript application/x-javascript application/xml; #设置需要压缩的数据格式
    gzip_vary on;

    location ~* \.(css|js|png|jpg|jpeg|gif|gz|svg|mp4|ogg|ogv|webm|htc|xml|woff)$ {
        access_log off;
        add_header Cache-Control "public,max-age=30*24*3600";
    }
}
```

## Related

- [tindy2013/subconverter](https://github.com/tindy2013/subconverter)
- [CareyWang/MyUrls](https://github.com/CareyWang/MyUrls)

## Contributing

PRs accepted.

Small note: If editing the README, please conform to the [standard-readme](https://github.com/RichardLitt/standard-readme) specification.

## License

MIT © 2020 CareyWang
