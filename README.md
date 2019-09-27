# learnvps
## VPS和域名

### VPS

#### VPS简介

- 自己理解VPS就是在国外买了一个电脑。其他官方解释自行谷歌。

#### VPS购买

- 网上关于VPS的服务商有很多，可以直接谷歌VPS服务商测评：https://www.10besty.com/best-vps-hosting-services/，这个文章详细的讲了各个VPS服务商。

- 我购买的是hostwinds，这个文章讲了原因：https://www.vps234.com/bandwagonhost-vps-blocked-use-hostwinds-vps/

- 购买hostwinds的教程：https://www.vps234.com/hostwinds-purchase-tutorial/

  - 买的时候是买的一个月的，系统是ubuntu.18的版本，地址选的是西雅图

- 购买后的一些操作：https://www.vps234.com/usa-vps-hostwinds-control-panel-tutorials/

  - 购买后第一时间把IP去控制台ping一下测试一下是否可用，或者直接进入这个网址：https://www.vps234.com/ipchecker/，将IP复制进入就可以测试了，如果都是绿色就是好的，如果不是就看一条。

  - IPping不通的解决办法：https://www.vps234.com/usa-vps-hostwinds-ssh-connect-error/

  - 上面的教程在**重装系统**之后记得再重启一下，然后再去网站测一次，如果还不行，再换，直到成功为止。
## 域名

- 买好VPS之后就可以买域名了

- 买域名 => 到GoDaddy上面买比较方便

  - 搜索GoDaddy会出现一个网址：https://sso.godaddy.com/?realm=idp&path=%2Fproducts&app=account

  - 可以直接微信登陆，然后会让输入邮箱，输入邮箱之后就可以直接开始买域名

  - 直接搜搜想要的域名名字就可以下单买

  - 付款的时候最好使用招商银行等比较大的银行，小银行步骤会比较复杂

  - 读完款之后就会跳到设置域名的地方

    

- 设置域名

  - 是一个表格形式的页面。类型自动前三个分别是A、CNAME、CNAME

  - 新手操作只要前两个就够了

  - 点击第一个，填入买好的VPS的IP，保存就好了

  - 点击第二个，填入`@`就好了

  - 到此为止，域名就买好并且设置好了。

    ​	

### VPS的其他设置（mac系统）

#### 登录远程机器

- 第一步命令：

  ```javascript
  # ssh root@+ip地址 ip地址就是刚刚的vps的ip地址
  ssh root@ip地址
  ```

- 第一步后会问一下问题，按`enter`进入下一步，会让输密码，这个密码和刚刚的IP地址在同一个地方，把密码复制粘贴回车就行，然后输入`exit`退出

- 在刚刚退出之后，重新输入`ssh root@ip地址`这个命令进入，输入密码，就会出现`Welcome to Ubuntu....`这句话，就表示已经登录到那台电脑上了。

- 输入一下命令查看自己的IP地址：

  ```javascript
  # 直接这个命令输入进入查看自己的IP地址
  curl api.ipify.org
  ```

#### 修改登录方式

- 每次的密码登录是不安全的，需要更改登录方式，将密码登录功能改为使用公私钥进行登录，设置完之后，将密码登录的方式彻底关闭。

- 接着刚刚的`curl api.ipify.org`之后的命令是`exit`先退出这个电脑	
