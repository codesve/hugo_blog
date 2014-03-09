{
	"Title": "ubuntu 11.10安装ruby开发环境",
	"Description": "",
	"Keywords": [
		"ruby",
		"ubuntu"
	],
	"Tags": [
		"ruby",
		"ubuntu"
	],
	"Pubdate": "2014-03-09",
	"Url": "code/test-code",
	"Slug": "ubuntu 11.10安装ruby开发环境",
	"Section": "code",
	"Thumbnail": "/uploads/2009/12/2668516894_1ca5eb1eed_m.jpg"
}

这次安装又有一些变化，记录一下：
1.先装一些必要的依赖包：
sudo apt-get install apache2 curl git libmysqlclient-dev mysql-server nodejs
2.安装RVM，命令有所变化了……
$ bash -s stable < <(curl -s https://raw.github.com/wayneeseguin/rvm/master/binscripts/rvm-installer)
这个命令是安装RVM。
echo ‘[[ -s "$HOME/.rvm/scripts/rvm" ]] && . “$HOME/.rvm/scripts/rvm” # Load RVM function’ >> ~/.bash_profile
这个命令是把RVM加到环境变量中去。
source ~/.bash_profile
这个命令是重新载入环境变量。
如果上面这样做了以后，每次打开shell都要重新source ~/.bash_profile的话，就执行：
echo ‘[[ -s "$HOME/.rvm/scripts/rvm" ]] && . “$HOME/.rvm/scripts/rvm” # Load RVM function’ >> ~/.bashrc
$ rvm requirements
这个命令是根据需要提示安装一些依赖包。比如Ruby就提示要执行以下命令：
sudo apt-get install build-essential openssl libreadline6 libreadline6-dev curl git-core zlib1g zlib1g-dev libssl-dev libyaml-dev libsqlite3-0 libsqlite3-dev sqlite3 libxml2-dev libxslt-dev autoconf libc6-dev ncurses-dev automake libtool bison subversion
这样RVM就安装完成了。
3.安装Ruby
rvm install 1.9.2
这会安装1.9.2版本的ruby，还可以执行rvm install 1.9.3安装更新版本。
rvm –default 1.9.2
这个命令是确定默认的ruby版本。
4.安装Rails
gem install rails
还可以执行以下命令安装特定版本的rails
gem install rails –version 3.1.0
如果安装了不同版本的rails，可以执行以下命令指定使用特定版本
rails 3.1.0 –version
end.