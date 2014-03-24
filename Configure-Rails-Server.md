###配置一台生产环境的服务器


####添加deploy用户

		sudo adduser deploy

####为deploy用户添加管理员权限

切换到 /etc sudoers 添加sudo用户

1. step1:切换到root用户；

2. step2:修改/etc/sudoers 文件编写权限：

		chmod u+w /etc/sudoers

3. step3:编译改文件：

		vi /etc/sudoers

   将：

		xxx ALL=(ALL) ALL 加入其中：

4. step4:
		还原/etc/sudoers 文件编写权限，并推出：
		chomd u-w  /etc/sudoers


	之后就可以sudo了；

####更换Ubuntu更新源

输入
		
		sudo vi /etc/apt/sources.list
		
加入网易的源

		deb http://mirrors.163.com/ubuntu/ precise main restricted universe multiverse

		deb http://mirrors.163.com/ubuntu/ precise-security main restricted universe multiverse
		
		deb http://mirrors.163.com/ubuntu/ precise-updates main restricted universe multiverse

		deb http://mirrors.163.com/ubuntu/ precise-proposed main restricted universe multiverse

		deb http://mirrors.163.com/ubuntu/ precise-backports main restricted universe multiverse


		deb-src http://mirrors.163.com/ubuntu/ precise main restricted universe multiverse


		deb-src http://mirrors.163.com/ubuntu/ precise-security main restricted universe multiverse

		deb-src http://mirrors.163.com/ubuntu/ precise-updates main restricted universe multiverse

		deb-src http://mirrors.163.com/ubuntu/ precise-proposed main restricted universe multiverse

		deb-src http://mirrors.163.com/ubuntu/ precise-backports main restricted universe multiverse

然后

		sudo apt-get update
		
#### 安装必要的三方库

		sudo apt-get install -y wget vim build-essential openssl libreadline6 libreadline6-dev libmysqlclient-dev curl git-core zlib1g zlib1g-dev libssl-dev libyaml-dev libxml2-dev libxslt-dev libcurl4-openssl-dev autoconf automake libtool imagemagick libmagickwand-dev libpcre3-dev nodejs libpq-dev
		
		
####安装RVM

执行

		curl -sSL https://get.rvm.io | bash -s stable
		
		echo '[[ -s "$HOME/.rvm/scripts/rvm" ]] && . "$HOME/.rvm/scripts/rvm"' >>~/.bashrc

		 source ~/.bashrc
		 
		 source ~/.bash_profile
		 
检查RVM 依赖更新 

		rvm requirement
		
####安装ruby

安装依赖

		rvm pkg install readline openssl
		
更换成国内的 RVM安装源(可选)
		
		 sed -i 's!cache.ruby-lang.org/pub/ruby!ruby.taobao.org/mirrors/ruby!' $rvm_path/config/db
		
		
查看RVM支持的的Ruby版本

		rvm list known

安装Ruby 

		rvm install 2.0.0		

####创建gemset

创建一个 4.0.2的 Rails 空间(就是我们说的gemset，方便在不同版本的ruby和rails中切换)

		rvm gemset create rails4.0.2
		

指定gemset的ruby版本并且设为默认

		
		rvm use 2.0.0@rails4.0.2 --default


#### 安装 Rails

替换 RubyGem换成淘宝镜像(主要是针对在国内的服务器)

		gem sources --remove https://rubygems.org/
		gem sources -a http://ruby.taobao.org/
		gem sources -l
		
安装指定版本的Rails

		gem install rails -v 4.0.2
	
####安装git

		sudo apt-get install git-core openssh-server openssh-client

		sudo apt-get install git-core git-gui git-doc 


* 第一个是git的安装包，其他的是git的依赖安装包

####安装RVM

