## AWS
	EC2
		reboot 
		stop restart后public IP会变化
		
		$ ssh ec2-user@13.239.19.231
		$ df -hT /dev/xvda1 查看EC2 EBS 使用量

	CloudWacth


## Docker 
	$ docker exec -it <69d1> bash 进入容器内部
	$ sudo service docker start


## Linux
	key
		// 安装openssh
		$ sudo apt install openssh-client 

		// 检查SSH key是否已经存在
		ls ~/.ssh/

		// 产生key
		ssh-keygen -t rsa -C "roger.qi.chen@gmail.com"
		/home/roger/.ssh/id_ras

		cat id_rsa.pub
		Import public key to EC2 Key Pairs





## CI/CD
	# Jenkins
	$ docker run --name jenkins -u root -d -v $(pwd):/var/jenkins_home -v /var/run/docker.sock:/var/run/docker.sock -p 80:8080 -p 50000:50000 jenkinsci/blueocean
	$ docker run --name jenkins -u root -d -v $(pwd):/var/jenkins_home -v /var/run/docker.sock:/var/run/docker.sock -p 81:8080 -p 50000:50000 jenkinsci/blueocean
	
	roger
	830521



## MySQL
   #查看版本
   mysql --version
   mysql -v
   select version();

   # 登录
   mysql -uroot -p
   mysql -uroot -p***

   # database
   show databases;
   create database dbname;
   use dbname;
   source D:\MySQL\bjpowernode.sql
   drop database dbname;
   select database(); 查看当前使用数据库

   # 表tables
   show tables;
   desc dept; 查表结构
   select *from dbname; 查表的所有字段


## Terraform
   $ terraform init
   $ terraform plan
   $ terraform apply


## 正则表达式
	r"" r开头
	[] e.g. r"r[au]n"
	[A-Z]	# 
		e.g. r"r[A-Z]n"
	[a-z]	#
		e.g. r"r[a-z]n"
	[0-9]	#
		e.g. r"r[0-9]n"
	[0-9a-z]	# 
		e.g. r"r[0-9a-z]n"
	\d 	# decimal digit 所有数字
		e.g. r"r\dn"
	\D 	# 
		e.g. r"r\Dn"
	\s
	\S
	\w
	\W
	\b
	\B
	\\ 匹配反斜杠
	.
	^
	$
	?
	*
	+
	{n,m}
	?P
	|

## Kubernetes
	# kind
		kind is a tool for running local Kubernetes clusters using Docker container “nodes”.
		kind was primarily designed for testing Kubernetes itself, but may be used for local development or CI.


	# kubectl
		The Kubernetes command-line tool allows you to run commands against Kubernetes clusters.
		Install: 
			curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"

		$ kubectl get pods
		$ kubectl exce 进入running container
		$ kubectl logs [NAME]


## Docker
	# 帮助命令
		$ docker version
		$ docker info
		$ docker --help

	# 容器生命周期管理
		$ docker run [container_name]
		$ docker run -it[image] [command] # 运行一个容器
			e.g. docker run hello-world
			e.g. docker run -it ubuntu bash
			e.g. docker run nginx
			e.g. docker run -d -p 80:80 --name demo nginxdemos/hello  # 从nginx demo image运行docker容器
		$ docker start / restart
			e.g. $ docker start [xxx]
		$ docker stop [container_name] # 停止容器
		  docker stop $(docker ps -aq) # 停止所有容器
			e.g. $ docker stop demo
		$ docker kill [container_name] # 杀掉一个运行中的容器
			e.g. $ docker kill demo
		$ docker kill [your_container_id] # ID	
			# stop和kill的区别：stop先给容器发送一个TERM信号，kill不管容器同不同意直接执行强制终止
		$ docker rm
			e.g. $ docker rm demo # 删除容器
		  docker rm $(docker ps -aq) # 删除所有容器
		$ docker pause/unpause
		$ docker create
			e.g. $ docker create xxx # 创建容器
	  		e.g. $ docker create centos:latest /bin/bash
		$ docer exec
		  docker exec -it[image] [command] # Execute command in a container
			e.g. $ docker exec -it demo sh # 进入容器并在内部执行命令
			e.g. docker exec -it bec5 bash

		# 容器内命令
			ls
			ps -ef
			whoami
			uname -a
			cd /etc/nginx/
			ls
			cat nginx.conf
			exit
	  		
	# 容器操作命令
		$ docker ps # 列出容器 list docker containers
		  docker ps -a # 查看隐藏容器
		  docker ps -aq
		$ docker inspect [container_name]
		$ docer top
		$ docker attact
		$ docker events
		$ docker logs [name] # Inspect the container
			e.g. $ docker logs demo
		$ docker wait
		$ docker export
		$ docker port
		$ docker cp your_file demo:/ # 拷贝一个文件到容器
	  
	# 本地镜像管理命令
		$ docker images # 列出本地镜像
		  -a: 列出本地所有的镜像（含中间映像层）
	      -q: 只显示镜像ID
	      -qa: 列出本地所有的镜像ID（含中间映像层）
	      --digests:显示镜像的摘要信息
	      --no-trunc:显示完整的镜像信息
		$ docker image list # 查看当前主机镜像列表
		$ docker rmi [image_name] # 删除image
		  docker rmi hello-world # 删除hello-world镜像
		  docker rmi $(docker images -q) # 删除所有镜像
		$ docker tag ID name # 标记本地镜像，将其归入某一仓库
			e.g. docker tag 618 hello
			e.g. docker tag ubuntu chenqi830521/myubuntu
		$ docker build . # .代表当前目录
		$ docker history
		$ docker image save centos > docker-centos.tar.gz # 导出镜像
		$ docker load
		$ docker import

    # 镜像仓库
	    $ docker login # login to Docker Hub
	    	chenqi830521
	    	48Perring
		$ docker build 
			e.g. $ docker build -t chenqi830521/test:1.0 .
		$ docker push 
			e.g. $ docker push chenqi830521/test:1.0
	    $ docker pull xxx # 根据镜像名拉取第三方镜像
			e.g. docker pull centos
			e.g. docker pull index.tenxcloud.com/tenxcloud/httpd
			e.g. $ docker pull  chenqi830521/test:1.0

		$ docker search

	# Docker Compose
		Install Docker Compose
			$ sudo curl -L "https://github.com/docker/compose/releases/download/1.25.0/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
			$ sudo chmod +x /usr/local/bin/docker-compose

			$ docker-compose build
			$ docker-compose up

	# Docker Swarm
	$ docker swarm init
	$ docker swarm join
	$ docker swarm leave --force
	$ docker swarm stack deploy -c
	$ docker-compose.yml your_stack_name
	$ docker stack ls
	$ docker service ls
	$ docker service create your_im age_name
	$ docker service ps [your_service_name]
	  docker service ps [your_service_id]
	$ docker service scale [your_service_name]=count
	$ docker service inspect [your_service_name]
	$ docker service rm [your_service_name]


## Python
	# 导入
	import xxx
	from xxx import xxx
	import xxx as x


	$ sudo ln -sf python3 python 修改python指向python3
		ln: 修改符号链接
		-s: soft 软链接
		-f: force 强制覆盖现有链接


## pip
	pip -V 版本确认
	pip list 列出本地安装包
	pip install [package_name] 包安装
	pip install -U [package_name] 包更新
	pip uninstall [package_name] 包卸载
	pip search [package_name]包检索(服务器端)
	pip freeze 输出安装包的详细信息
	pip show 显示本地安装包的详细信息
	pip install --upgrade pip 自身更新
	pip help 帮助信息


## virtualenv
	pip3 install virtualenv 安装虚拟环境
	virtualenv [project_name] 创建项目虚拟环境目录

	#Linux
	$ source [project_name]/bin/ 激活虚拟环境
		(e.g. source DevOps/bin/activate)
	$ workon [project_name]
	$ deactivate 退出虚拟环境

	#Windows
	> [project]\Scripts\activate 启动
	> deactivate 退出虚拟环境
	> pip freeze > requirements.txt 导出包
	> pip install -r requirements.txt 安装包


## virtualenvwrapper
	$ mkvirtualenv [project_name]
	$ workon


## Git & GitHub命令
	git --version
	git init
	git status
	git config user.name tom_pro
	git config user.email chenqi830521@gmail.com
	git config -global user.name tom_pro
	git config -global user.email chenqi830521@gmail.com

	# Local repository
		$ git add [file name] 从工作区提交到暂存区
		$ git commit [file name]
			$ git commit -m "Comment" [file name] 从暂存区更新到本地库
			$ git commit --amend 再次修改，重新add后commit，这样就还是一条log信息

		$ git log 
			$ git log --oneline 一行打印
			$ git reflog
		$ git reset 前进或回退到某个版本
			$ git reset --hard[局部索引值] 工作区，暂存区和本地库三个区都跳到指定版本
			$ git reset --soft[] 工作区和暂存区不同步，只有本地库跳到指定版本
			$ git reset --mixed[] 暂存区同步，工作区不动

	# Remote repository
		$ git clone [url] 克隆整个项目到本地（不用mkdir项目文件夹）
			e.g. $ git clone https://github.com/chenqi830521/hello-Jenkinsfile.git
		$ git pull 拉取最新（需要cd进入项目文件夹）
			$ git pull = fetch + merge
		$ git push 提交到远程库
		$ git branch 类似ls，列出当前所有分支
		$ git branch [分支名] 创建分支
			$ git branch -v 显示更多信息
		$ git checkout [分支名] 切换分支
			$ git checkout master 切换到主分支
			$ git checkout -f
			$ git checkout -b "new-branch-name" 创建并切换到新的分支
			$ git checkout integration

		$ git fetch 远程库下载到本地库，但工作区中的文件没有更新
		$ git rebase 变基，整合分叉的历史，可以将某个分支上的所有修改都移到另一分支
		$ git merge [分支名]

	git rm --cached [file name]
            git rm -r FolderName git commit -m “Delete FolderName” git push 
	git co master
	git st
	git stp
	rm -rf test
	git log –pretty=oneline
	git log --oneline
	git reflog
	git revert
	git remote add upstream
	git fetch upstream 
	git 
	squash
	fast forward

## Linux路径
	~（潮水符号）：这是home文件夹的快捷表示。如果你的家文件夹是/home/ryan,那么你就可以通过/home/ryan或~来操作这个文件夹。

	.(点)：这代表你现在所处的文件夹位置。在上面的例子上，我们在相对路径下操作Document文件夹，我们也可以通过./Document来进行处理。（或许你现在觉得没有必用，但是之后我们会发现这是一个不错的选择）。

	..(两点）：这代表你所处的文件夹的上一级文件夹。你可以多次使用这个快捷表示，一直让你的位置往根文件夹走。例如你现在是在/home/ryan这个位置上，你可以用ls ../../ 去显示根文件夹下的文件。

	/ 根目录

## Linux目录结构
	/bin User Binaries系统bin,如ls, cp, cd等命令，所有用户都可以使用
	/sbin System binaries
	/usr User Programs
		/usr/bin
		/usr/sbin
		/usr/lib 
	/root 
	/home Home directories 用户自己的data
		/home/vagrant home下的用户
	/etc Configuration files 系统配置文件
		/etc/nginx
		/etc/resolv.conf
		/etc/host.conf
	/lib System libraries shared libraries
	/tmp Temporary Files
	/mnt Mount directory
	/srv Service data
	/var 
	/dev Device Files 管理设备
	/media Removable devices 目录
	/opt Optional applications 
	/boot Boot loader files 启动Linux需要的启动程序
	/proc[别动] Process Information 这个目录是一个虚拟的目录，它是系统内存的映射，访问这个目录来获取系统信息
		/proc $ less cupinfo


## Linux指令
	# 常用
		$ ls:列出目录
			$ ls -altr 按照时间排序
			$ ls -1A 隐藏文件
			$ ls -l|less 管道操作分屏查看
			$ ls -l
		
		$ pwd 当前路径

		$ cd . 回到本级目录
		$ cd .. 返回到上一级目录
		$ cd ~ 回到Home目录
		$ cd [direct name]
		$ cd / 根目录，可以ls查看根目录的内容

		$ mikdr
		$ mikdr -p  ../xxx/xxx/xxx

		$ touch test.txt

		$ cat xxx.xxx 查看文件内容 
			cat /proc/cpuinfo
			cat /proc/meminfo

		$ rm test.txt

		$ less

		$ dmesg 
		$ dmesg | less -p "failure" 竖线的意思：把上个命令的结果传给下一个命令

		# Tips
			Ctrl + R
			Tab
			上下键
			Ctrl + a
			Ctrl + e
			
	# Redirection
		# cat > list1


		# sort 





	# 端口
		$ sudo netstat -npl | grep 80 # 查看使用80端口
		$ lsof -i :80| grep LISTEN # 释放被占用端口

	$ echo ‘abcdeABCDE’ > a.txt
	$ locate *.jpg
	$ locate -i *.jpg
	$ find . -name report.txt
	$ find . -type f -exec grep
	$ grep -i -r "find" .
	$ grep find search.sh
	$ ls  /usr/lib | grep docker
	$ history | grep "bash"
	$ dmes


	
	$ chmod
		$ chmod 755 hello.sh
		$ chmod root hello.py 将owner改成root

	$ man 
		$ man ls ls帮助
		$ man chmod 
	$ sudo su 变成root用户
	$ less 
		$ less --help
		$ less 



	$ sync 同步内存
	find / -name [file_name]
	ll：


	$ ssh 登录远程主机host
		$ ssh -i identity_file 从指定文件中读取传输时使用的密钥文件，此参数直接传递给ssh
		$ ssh -i "ubuntu.pem" ubuntu@13.239.6.141

	head:查看文件头几行内容
	head -n 2 text1: 查看text1的头两行
	tail:查看文件最后几行内容
	tail -n 2 text1：查看text1的最后两行
	df -h
	shutdown -h now
	sudo apt install -y apache
	cd:切换目录
	cd ..:回到上一层
	pwd:显示目前的目录
	mkdir [Dricety Name]	建立新的目录
	cp:复制文件或目录
		(e.g. cp text1 ../demoshow2)
	rm:删除文件或目录
	rm -rf: 删除所有文件 例如：rm -rf text1
	mv:移动文件、文件夹或修改名称
	nano

	#
	1.每个命令之间用;隔开
	说明：各命令的执行给果，不会影响其它命令的执行。换句话说，各个命令都会执行， 但不保证每个命令都执行成功。
	2.每个命令之间用&&隔开
	说明：若前面的命令执行成功，才会去执行后面的命令。这样可以保证所有的命令执行完毕后，执行过程都是成功的。
	3.每个命令之间用||隔开
	说明：||是或的意思，只有前面的命令执行失败后才去执行下一条命令，直到执行成功 一条命令为止。
	
	# wget 下载
	wget https://nginx.org/download/nginx-1.17.9.tar.gz
	wget -c 支持断点续传下载
	wget -c https://nginx.org/download/nginx-1.17.9.tar.gz

## 常用的DOS命令
	dir 查看目录下的文件（夹）
	ca 进入到指定的目录
	cd. 表示当前目录
	cd.. 表示上一级目录，cd .. 
	md 创建一个目录
	rd 删除一个目录
	del 删除一个文件 del abc.txt
	cls 清除屏幕

## Vagrant
	vagrant up
	vagrant ssh
	vagratn ssh -- -X # 此种方式可以打开Firefox等
	vagrant reload
	vagrant scp <local_path> [vm_name]:<remote_path>
		(e.g. vagrant scp requirements.txt /home/vagrant/)
	vagarnt box 

## AWS
	aws configure
	aws configure –profile default
	
	# S3
	$ aws s3 ls
	$ aws s3 mk s3://xxx
	$ aws s3 rb s3://xxx
	$ aws s3 cp /xxx/xxx s3://xxx
		(e.g. aws s3 cp /etc/nginx/sites-availabel/default s3://roger-demo)
	$ aws s3 ls s3://xxx
		(e.g. ws s3 ls s3://roger-demo)
	$ aws s3 sync . s3://xxx
	$ aws s3 sync /xxx/xxx s3://xxx

    # Cloudformation
    $ aws cloudformation create-stack --stack-name <value> --template-body <value> (e.g. aws cloudformation create-stack --stack-name myBucket --template-body file://s3-bucket.json)
    $ aws



