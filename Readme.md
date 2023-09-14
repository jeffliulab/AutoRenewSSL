[NOT FINISHED YET]【还未完成】

项目的目的：录入网站的关键信息后，可以实现脚本一键完成SSL登录。（使用免费的openssl）

Keywords: Godaddy, Letsencrypt, SSL
Environment: Cpanel，Linux, .acme.sh
This project is help those who use Godaddy to create a letsencrypt SSL. Let's Encrypt recommends generating your certificate through Certbot but this is not supported on GoDaddy's cPanel Linux hosting. 

在摸索了一天后，终于手工部署好了SSL，现在总结一下手动过程：
1、在cpanel中设置ssh连接
2、使用mac的terminal，进行ssh连接，访问服务器
3、安装acme.sh
4、输入指令：acme.sh --issue -d 网址 --webroot /home/用户名/public_html/ --server letsencrypt
5、安装好后，使用ftp工具访问网站的目录，找到cer文件
6、使用cd命令将目录调整到cer文件所在文件夹
7、使用x509命令将cer文件转换为crt文件
8、登陆cpanel，手动上传crt、key，并install ssl（自动填入）
9、最后在cpanel的domain中勾选强制https。或者在网站中添加.htaccess file。

将上述过程改为自动脚本，自动化过程规划如下：
前置：cpanel中设置api
1、通过python实现ssh连接、ftp连接、访问cpanel的api
2、在python脚本中通过ssh连接服务器
3、通过python安装acme.sh
4、通过python安装cer证书
5、通过python将cer证书转换为crt证书
6、将crt和key上传并install ssl
后置：在cpanel的domain中勾选强制https
