一、Alwaysdata.com 介绍

Alwaysdata 是一家来自法国的虚拟主机服务商，除了收费主机，也提供免费虚拟主机，支持 PHP5、CGI（Perl5）、Python、Ruby 动态程序，可创建无限个 MySQL、PostgreSQL 数据库，FTP、Web 方式上传管理文件，还提供了 SSH、WebDAV 权限。当然，使用 Alwaysdata 也可以完美搭建 v2ray 节点。

Alwaysdata 官方文档：https://help.alwaysdata.com/en/

二、注意事项

对于任何一个云开发平台，挖矿和流量代理项目都是不受欢迎的，属于滥用行为。建议可以将 Alwaysdata 作为防失联用途使用，科学上网主线路可以使用付费的 vps 。我前一段时间在 telegram 群里为大家推荐的 Gcore 200M 带宽不限流量套餐，每月 3.25 欧元，折合人民币 24 元左右，我觉得大多数人都可以承受。提醒各位小伙伴，本项目仅限技术交流使用，请勿滥用，由此引起的账号封禁等风险自负。

三、GitHub 项目地址

https://github.com/hiifeng/V2ray-for-AlwaysData

四、注册并登录 Alwaysdata.com

Alwaysdata.com 注册很简单，只需要一枚邮箱即可。

官方地址：https://www.alwaysdata.com/en/register/

1-Create my profile.webp

五、v2ray 节点搭建

1、登录 Alwaysdata 后，会出现如下界面，我们参考如下图片创建一个实例。如果在创建过程中系统提示“This name is not valid. Please choose another one.”，说明你填写的 Name 已经被占用，请重新更换一个。这里填写的 Name 与 password 为 SSH 、FTP 的登录用户名与密码。

2-Create an instance.webp

2、创建好实例后，我们点击左侧菜单 Web -> Sites ， 然后点击右侧的齿轮按钮，配置你所创建的实例。

3-edit.webp

3、修改 Configuration 中的 Type 为 Static files ，同时在 Advanced Settings 中填写如下代码，最后点击底部的 Submit 。

Bash
#UUID=de04add9-5c68-8bab-950c-08cd5320df18
#VMESS_WSPATH=/vmess
#VLESS_WSPATH=/vless
注意：这三行代码的用途为自定义 UUID 和伪装路径。其中 "VMESS_WSPATH" 和 "VLESS_WSPATH" 变量分别代表 vmess 的伪装路径和 vless 的伪装路径， 需要以"/"符号开头， UUID 可以使用 第三方工具 生成。

4-Configuration.webp

4、点击左侧菜单 Remote access -> SSH ， 记住右侧顶部为你的实例分配的 ssh 域名，下一步会用到。然后点击齿轮按钮，修改你所创建的实例的 SSH 配置。

5-ssh.webp

5、选中 Enable password login 前的复选框，然后点击底部的 Submit 。

6-Enable password login.webp

6、使用 ssh 工具登录实例后，执行如下命令，安装 v2ray 。

Bash
bash <(curl -sL https://raw.githubusercontent.com/hiifeng/V2ray-for-AlwaysData/main/install.sh)
7-install v2ray.webp

7、上一步命令执行完成后，会出现如下提示。

8-config info.webp

8、我们根据提示，配置一个 Services 。首先点击左侧菜单 Advanced -> Services ， 然后点击右侧的 Add a service 按钮。

9-Add a service.webp

9、如图所示，将如下命令复制到 Command* 中，然后点击底部的 Submit 。

Bash
./v2ray -config config.json
10-config service.webp

10、再次点击左侧菜单 Web -> Sites ， 然后点击右侧的齿轮按钮，配置你所创建的实例。

11-config sites.webp

11、将第 7 步生成的 Advanced Settings 信息 copy 到文本框中，然后点击底部的 Submit 。

12-Advanced Settings.webp

12、打开第 7 步程序创建的网址，可以得到 vmess / vless 的节点链接和二维码。将节点链接导入 v2rayN 或使用手机扫描提供的二维码即可以科学上网。

13-v2ray link.webp

六、使用 Cloudflare CDN 对 Alwaysdata 节点进行提速

14-speedtest.webp

通过测试， Alwaysdata 分配的 IP 地址在法国，目前平台分配的域名还可以正常使用，以上截图是没有套 CF 的测速情况，个人感觉晚高峰时速度不是很理想，建议配合 Cloudflare CDN 使用。可以使用 CF 的 Cname 、worker 、pages 任意一种方式。具体教程可参考以下文档：

https://www.hicairo.com/post/59.html
