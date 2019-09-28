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

- 输入以下代码：

  ```javascript
  #输入这个命令后会有一个选择 意思是是否需要把生成的公私钥保存到一个文件/.ssh/id_rsa里面 
  #如果已经存在id_rsa，会问你是否需要覆盖 选择NO
  ssh-keygen
  ```

- 输入下面代码：

  ```javascript
  # 这个命令的意思是把上面生成的密钥复制到你的那台远程机器上 让远程电脑设定并登陆 并信任这个公钥
  ssh-copy-id root@muee.me
  ```

- 输入下面代码：

  ```javascript
  # 尝试再次登陆这个机器 看下是否还需要输入密码 如果不需要输入密码就登陆成功 就说明刚刚上面的几步操作成功
  ssh root@muee.me
  ```

- 在远程机器上有一个文件夹`.ssh`里面有个文件`authorized_keys`，这个文件里面存放了远程机器信任的公钥列表。

- 可以输入命令`cd .ssh   => l  => vi authorized_keys`进入这个文件看到复制过来的公钥

#### 关闭密码功能

- 经过上面的步骤已经将公私钥登陆的方式设置好了，这时候我们再去将密码登录功能进行关闭

- 可以直接搜索`ssh 关闭密码功能登录`，找到相关的信息。

- 先登录到远程机器

  ```javascript
  ssh root@muee.me
  ```

  

- 将/etc/ssh/sshd_config，里面的PasswordAuthenticatiion改为no,ChallengResponseAuththentication改为no,然后**重合sshd（service sshd restart）**后就可以了。

  ```javascript
  # 进入这个文件 按 i 这个键进入输入模式 找到上面需要更改的两个地方进行更改 更改完之后按 esc 键退出输入模式
  # 然后再按 :wq! 保存并退出这个文件 就改好了，一定要记得重启 否则不会生效 
  vi /etc/ssh/sshd_config
  ```

- 经过上面的步骤，我们已经成功的关闭了密码功能，不用再担心被黑客黑掉

#### 修改默认端口号

- 系统默认端口号是22，为了避免黑客撞库攻击，我们应该将端口号设置为其他的端口号（小于65538的数字都可以）

- 再次进入文件：

  ```javascript
  #还是和上步操作方法一样 找到port 去掉# 然后直接修改好保存并退出 然后重启一下服务重合服务：sshd（service sshd restart）就生效了
  vi /etc/ssh/sshd_config
  ```

#### 快捷登陆方式

- 我们现在登陆需要输入`ssh root@muee.me`这个命令，实际上可以直接`ssh m`这个命令登陆。

- 先输入`exit`退出远程机器

- 退出远程机器之后，输入` cd ~/.ssh/`进入.ssh文件夹下，找到config文件，如果没有，可以自己新建一个这个名字的文件，`vi config`进入文件输入以下内容：

  ```javascript
  HOST m  # 别名 想要以什么名字登陆 ，字母和数字都可以
  	HostName muee.me #真正的域名
    User root #用户名
    Port 10086 #端口号 小于65538都可以
  
  ```

- 然后保存退出。重新用设置的`ssh m`来进行登录，如果登录成功，表示这个步骤设置成功。

#### 装Node软件

##### 第一种方法：

- 很遗憾node这个不是自带的，需要自己装，可以运行`node -v`会发现提示`Command  'node' not found,but can be installed with: apt install nodejs``,意思是可以用`apt install nodejs`来装node，但是使用这个安装node并不是最新版的，我们需要自己手动安装最新版本。

- 先找到node官网：https://nodejs.org/en/

- 找到`Other Downloads`即下面这个网址：https://nodejs.org/en/download/current/

- 往下拉找到：[Installing Node.js via package manager](https://nodejs.org/en/download/package-manager/)

- 点进去之后找到[Debian and Ubuntu based Linux distributions, Enterprise Linux/Fedora and Snap packages](https://nodejs.org/en/download/package-manager/#debian-and-ubuntu-based-linux-distributions-enterprise-linux-fedora-and-snap-packages)

- 找到[Official Node.js binary distributions](https://github.com/nodesource/distributions/blob/master/README.md) 会进入到https://github.com/nodesource/distributions/blob/master/README.md

- 找到Installation instructions，下面就是nodejs的版本，然后会看到相对应版本的各种命令代码：

  ```javascript
  # Using Ubuntu
  curl -sL https://deb.nodesource.com/setup_12.x | sudo -E bash -
  sudo apt-get install -y nodejs
  ```

- 搞完上面这个命令之后就可以装上最新版本的nodejs

- 输入`node -v`测试是否有显示版本号，如果显示版本号说明成功装上。

##### 第二种方法

- 谷歌搜索`nvm`,或者直接进入这个网址https://github.com/nvm-sh/nvm，找到`Install & Update script`，复制下面的命令：

  ```javascript
  curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.34.0/install.sh | bash
  ```

- 输入这个命令之后，输入`exit`退出远程机器，然后重新进入远程机器，输入`nvm`看到一大堆信息就表示成功了。

- 装了nvm之后会把之前装的node版本替换掉，输入以下命令再替换回来

  ```javascript
  nvm install node@12.10.1 
  ```

- 再输入`node -v`就会发现已经替换回到最新版本12.10,1，再输入`npm -v`会发现这个也变成最新的版本。

以上步骤就完成了node的安装。


