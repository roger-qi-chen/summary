ssh ec2-user@3.25.160.224


git fetch && git checkout OAP-9

Git Visualizing 
https://git-school.github.io/visualizing-git/
 
2月22日Onboarding
17年成立
Adelaide Street
项目开发
移动端开发
UI/UX
工作：完善一些项目，开发一些新的系统
周一 - 周五 10a.m-6p.m
请假： 3-以上 提前申请
2天以内 提前1天
请假邮箱：career@jiangren.com.au
需要向老板
3个月实习时间 原则上不可以提前离职
提前一周跟老板说
 
 
BA
官网就是一个产品
也会推出新产品
PR
另一个产品：LMS
UAT Merge 到UAT
notion.so
2个星期 是一个Spring
11点 Standing meeting
Aglie
Ticket
Re
 
达到 80 story point
zepin

2月23日
Standup meet
说的多一点 不要说减分的东西
把一天做过的东西
看了个项目 做了research and invensment
认识了BA 
今天的计划
onboarding
data flow, 逻辑

Junior 不是entre level
Mid Feature开发
Senior 

EC2 AWS
E2E testing

UAT BA和
intergation 

Local 到 UAT  Dev 和 Sener
从UAT 开始进入

UAT staging production(2 3个数据库)
red server 
blue server 
切换URL 

ECS 

设计 开发 调度

SRE

QA Automati test
E2E Test
PO（P Owner）QA
UAT（User Accept Testing）

1个Sp 2个星期 8分

Jenkins部署

2月25日
Standup meeting 
1 了解了一下公司官网啊，LMS等产品和现行项目比如OA啊,OAP啊,官网。
2 也了解了一下Jira上的各项目以及个项目的Tickets，对应的Story Point等，主要了解了一下JRWeb02项目的Tickets，并和开发的同学一起参与了JRWeb02的refine meeting。
3 因为我们的官网是放在Asia Pacific Region的 Sydney Availabilty Zone(ap-southeast-2)学习了AWS新的UI上FrontCloud和Route53对CDN，DNS的设置，计划通过AWS提供的Infrasturcture AS Code的工具FrontFormation用yaml file的方式，也是DevOps的方式去。
4 今天计划了解一下公司官网在AWS上的整体架构。
5 计划学习一下如何在AWS的EC2上搭建一个Jenkins Server用于我们OAP以及后续项目的持续集成和持续部署,也就是我们说的CI/CD。希望哪位开发OAP的同学帮我介绍一下OAP项目。


尹航
Application 到YAML
RDS(Relational Database Service) 太贵
因为主要是题和答案
疑难解惑
Logging 信息 
记录到RDS


sg Webstorm InteliJ 
git rebase 把前面的commint 合并成一个
比如简历功能的branch
feature branch
单独的UAT
hot fix


2月26日
Standup meeting 
1 学习了Git https://git-school.github.io/visualizing-git/

2 Travis CI https://www.travis-ci.com/
https://travis-ci.org/




2 比较了一下Jenkis的各种安装方式：
Master Node
Common options to install Jenkins 
1. Official - https://jenkins.io - java -jar jenkins.war 
2. Docker - https://hub.docker.com/r/jenkins/jenkins/ 
3. Kubernetes - Kubernetes application - helm helm install --name jenkins stable/jenkins --set rbac.install=true \ --set Persistence.Enabled=true \ --set Persistence.StorageClass=jenkins-pv 
4. Configuration Management Tool: Chef, Puppet, Ansible or Saltstack 
5. Use Jenkins in the Cloud: CloudBees(https://www.cloudbees.com/), bitnami(https://bitnami.com/)

https://zhuanlan.zhihu.com/p/59686072

3 比较了一下 在AWS上安装Jenkis的几种方式：
EC2
       First, the traditional deployment on top of Amazon Elastic Compute Cloud (Amazon EC2) barebone machines. This approach is just like installing Jenkins on a local server, it comes with the traditional pros and cons.
      自己Launch EC2安装和配置Jenkins
Prerequisites
Create a key pair using Amazon EC2 if you already have one, you can skip this step
Create a security group for your Amazon EC2 instance if you already have one, you can skip this step
Launch an Amazon EC2 instance
Install and configure Jenkins
Clean up
需求：key pair 和
           security group

1 创建了VPC SUBNET Internet Gateway  Route Table for Jenkins Server from VPC Dashbord on AWS
jiangren-jenkins-vpc
10.0.0.0/24
DNS hostnames: enable

jiangren-jenkins-subnet
AP-southeast-2c
	CIDR block 10.0.0.0/16
2 创建key pair 和 Security Group for EC2
cat ~/.ssh/id_rsa.pub
import public key
2.1 手动Launch EC2 注意选择enable public ip
2.2 Create EC2 from YAML file ia CloudFormation， t2.micro 名为jenkins的 
3 SSH到EC2
$ ssh ubuntu@172.31.0.253  OK
4 安装Docker
sudo yum update -y
sudo amazon-linux-extras install docker
sudo service docker start
https://docs.docker.com/engine/install/ubuntu/
5 安装Jenkins
https://github.com/JiangRenDevOps/DevOpsLectureNotesV3/tree/master/WK3_CI-CD-Jekins/1.Install-Jenkins-Docker
$ mkdir jenkins_home
$ cd jenkins_home
$ sudo docker run --name jenkins \
           -u root \
           -d \
           -v $(pwd):/var/jenkins_home \
           -v /var/run/docker.sock:/var/run/docker.sock \
           -p 80:8080 \
           -p 50000:50000 \
           jenkinsci/blueocean 
4 通过IP访问
Public IP:8080 例如： http://54.79.65.130:8080
$ sudo -su
$ sudo cat secrets/initialAdminPassword
ffb81d646ea9450892bf279da151c3a5
安装Plugins：Blue Ocean, Kubernetes plugin, Docker Pipeline





ECS
The second is the containerized deployment that leverages Amazon EC2 Container Service (Amazon ECS). Using an extensive plugin system, Jenkins offers options for integrating with many AWS services and can morph to fit most use cases (e.g., traditional development pipelines, mobile development, security requirements, etc.). While the white paper suggests using EFS in a containerized system, we are going to work around it because of the region we are in (ca-central-1)
ECS Cluster
1 Certificate Management -  Create Domain name:  .jiangren.com
Get ARN
2 CloudFormation 
YAML file from S3
Amazon S3 URL: https://xxx. jenkins-for-ecs.yml
Stack name: jenkins-for-ecs
CertificateArn: copy from step 1
Next
3 Tick I acknowledge and Next
4 ECS 
Cluster - Default-cluster - Task
Copy password
5 LoadBalance xxx.
6 
DNS Provider
CNAME  jenkins
https://jenkins.jiangren.com
7 Clean up
CloudFormation - Stact




deploy Jenkins into the AWS Elastic Container Service (ECS)
https://tomgregory.com/deploy-jenkins-into-aws-ecs/
https://tomgregory.com/deploy-jenkins-in
Making an Autoscaling Jenkins CI Cluster on Amazon ECS
https://anupam-ncsu.medium.com/making-a-jenkins-ci-cluster-on-amazon-ecs-5a03fac13773
CodeBuild 和 CodeDeploy
Elastic Kubernetes Service (Amazon EKS)
Setting up a CI/CD pipeline by integrating Jenkins with AWS CodeBuild and AWS CodeDeploy
需求和代码Repo连接起来,所以需要connect Online Assessment Platform(OAP)项目, 需要这个项目的用户名和密码

2月26日
Standup meeting 
1.昨天search了一些资料，比较了一下在AWS上set up Jenkins Server的两种常用方式：
一种是Launch一个EC2上直接装上Jenkins 作为一个Master Node来使用。
第二种是使用AWS提供的ECS（AWS Elasitc Container Service）服务创建一个可以Autoscaling Jenkins Cluster的。也可以用LoadBalance来分流Traffic，在一些

2. 创建了Jenkins Server 用的VPC, Subnet, Internet Gateway, Route Table，Key Pair，Security Groups等，并作了各种设置和连接。

并且用第一种方法通过AWS Console, launch了一台EC2, 是一台t2.micro level的Linux Machine, 安装了必要的依赖，并且使用Docker的方式安装了Jenkins以及需要用到的Plugin,我们可以通过public IP远程访问到这个Server。不过目前没有需求，担心产生额外的费用，目前是stop状态，需要用的时候我们可以再打开。 
也想跟老板确认一下，咱们目前是不是先用EC2的方式就可以，先不用考虑LoadBalance和 AutoScaling？

C级价格比较低的
$0.01左右的

3. 不过这台EC2是手动在Console创建的，并不是用YAML File Template的方式通过代码创建，这并不是一个好的DevOps way。昨天写的YAML File的代码貌似有点小问题，目前还没有解决。解决后就可以通过代码的方式创建EC2等Cloud 资源。计划今天再fix一下bug。

4.  也非常感谢尹珩，给我分享了很多OAP项目相关的信息，计划今天研究一下trigger OAP项目的代码，以及通过Jenkins部署React, Springboot以及PostgreSQL方面。 

需求和代码Repo连接起来,所以需要connect Online Assessment Platform(OAP)项目, 需要这个项目Repo的连接。

RDS 

EC2 


数据库用于IO和储存
数据库放在Docker里

EUT PRO
EC2的数据库
内存+CPU
数据量比JR学院

On the Choose an Amazon Machine Image page, select Free tier
only, and then select an Amazon Linux 2 AMI with the HVM virtualization
type.

t2.large
m3.medium
m4.large
m4.xlarge
m4.2xlarge

AWS Pricing Calculator

Part 1 Building a Spring Boot application in Jenkins.
Declarative Checkout SCM - Build - Test
Creating a Spring Boot application
GET/ride
GET/ride
POST/




Part 2 Building a Spring Boot application in Docker with Jenkis.
	Declarative Checkout SCM - Build - Test - Build Docker image - Push Docker image（Docker Hub）

Part 3 

3月1日
Standup meeting 
1 这几天一直在比较不同type EC2的价格。

2 调查了一下，C系列也就是计算优化型, 最便宜的也是0.0444 USD/hour。
   通用型也就是我们常用的t系列，因为t2 t3会有un lim Burstable Performance
   可以把credite specifcation 选成standard 不是unlimited 貌似CPU就不会burst

3 想尽快把ec2 type定下来，把Jenkins server set up起来。

4 计划写和J C一起研究一下LMS admin.jiangren.com.au前端的部署。
  计划从Bitbucket build 成 Docker Image 上传到 Docker Hub 然后从Docker Hub
  Jenkinsfile 怎么写，设置Elasit Beanstalk Envornment


在EC2部署了DB: DynamoDB
前端没有安全性可言
Yingjie Wang

super admin
postmain 
普通用户Read的权限
No SQL 冗余数据较多 垃圾数据很多
SQL DB 查询比较快


1 确定了EC2 type, 使用了t3a.small,并且Launch的时候取消了Credit specification的勾选,也就关闭了CPU burst，确保不会产生额外的burst performance的费用。

2 安装Docker
https://docs.aws.amazon.com/zh_cn/AmazonECS/latest/developerguide/docker-basics.html
$ sudo yum update -y
$ sudo amazon-linux-extras install docker
$ sudo service docker start
$ sudo usermod -a -G docker ec2-user
$ docker info

3 访问3.106.137.158

4 $ sudo cat secrets/initialAdminPassword
0b23e12e140c453da6d380ebe9fac6e1

5 安装Plugins：Blue Ocean, Kubernetes plugin, Docker Pipeline

6 学习bitbucket-pipeline
https://medium.com/@ericpwein/deploying-a-react-app-to-amazon-s3-with-bitbucket-pipelines-d93df3a324f9


# This is a sample build configuration for JavaScript.
# Check our guides at https://confluence.atlassian.com/x/14UWN for more examples.
# Only use spaces to indent your .yml configuration.
# -----
# You can specify a custom docker image from Docker Hub as your build environment.
image: node:10.15.3

pipelines:
    branches:
        master:
            - step:
                  caches:
                      - node
                  script:
                      - npm install
                      - npm test
                      - npm run build-uat
                  artifacts:
                      - dist/**
            - step:
                  name: Deploy
                  deployment: uat
                  script:
                      - pipe: atlassian/aws-s3-deploy:0.2.4
                        variables:
                            AWS_ACCESS_KEY_ID: 'AKIAIPIFCSS44LRCPUWQ'
                            AWS_SECRET_ACCESS_KEY: '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'
                            AWS_DEFAULT_REGION: 'ap-southeast-2'
                            S3_BUCKET: 'uat-learn.jiangren.com.au'
                            LOCAL_PATH: 'dist'
                            ACL: 'public-read'
                            CACHE_CONTROL: 'max-age=3600'
                            DELETE_FLAG: ‘true’

7 Jenkinsfile
https://medium.com/faun/ci-cd-pipeline-with-jenkins-and-aws-s3-c08a3656d381

8 安装role插件






9 
3月2日
Standup meeting 
1 确定了EC2 type, 使用了t3a.small,并且Launch的时候取消了Credit specification的勾选,也就关闭了CPU burst，确保不会产生额外的burst performance的费用。
    通Docker安装了Jenkins，并且做了简单的测试。
谁要用？
DNS Provider
CNAME  jenkins
https://cicd.jiangren.com.au
2 跟着JC同学学习了Bitbucket-pipeline CI/CD的流程，也学习了yml file的写法，因为之前都是用Jenkins。 
3 目前在写uat admin Jenkinsfile，以及设置Jenkins trig Bitbucket.

Zeplin 设计
comments
reviewer


Bitbucket
UAT
Web hook

Give Jenkins Authenticate to AWS with the Pipeline AWS Plugin 


安装Bikbucket plugin









3月3日
Standup meeting 


Jenkins设置
1 需要Bitbucket的Credential
2 Source Code Management
https://bitbucket.org/roger-qi-chen/ci-cd_test/
选择Credential
3 Build when a change is pushed to BitBucket 打钩
   POLL SCM打钩

Bitbucket设置
Repo setting - Webhook
Title: Jenkins Webhook
URL: http://cicd.jiangren.com.au/bitbucket-hook/
         http://cicd.jiangren.com.au/github-hook/

Jenkins凭证管理
https://www.cnblogs.com/FLY_DREAM/p/13888423.html

3月4日
Standup meeting 
1做了Jenkins Server的DNS设置和域名解析，目前可以通过cicd.jiangren.com.au 访问。
2 做了Jenkins 和 Bitbucket 的integraton,并且在Bitbutcket里设置了webhook， Jenkins可以自动trigger， 一旦Repo里有变化，就可以自动build。
3 在Jenkins上建了Pipeline，做了Jenkins Upload S3的试验，install 依赖，test 和build stage.


S3 publisher
https://blog.51cto.com/wzlinux/2483284


3月4日
Standup meeting 
1 昨天我修改了一下向AWS S3部署这部分的代码，刚开始遇到了一些问题，像credential，上传文件的路径等，在老板的指导和提示下，加上最后查了很多资料，最后解决了这个问题，用工程目录下的一个文件夹做了测试，把文件成功上传到指定的S3中，算是实现了在Jenkins Pipeline向AWS部署这个一个小部分。从这个过程也学习到了：Jenkins Output提示出的文件目录其实是运行Jenkins 这个docker contianer的内部的目录，因为这个Jenkins是用容器安装的，他是运行在容器里的，所以必须进到cotainer内部才能看到，并不在EC2 Linux Machine的Jenkins-home所在的目录。

2 计划今天继续完成剩余部分Pipeline的script，安装node.js 12.13.0, 安装依赖，以及build, 这部分可能会有写不懂的地方，需要跟一些developer了解和学习一下。

3 再一个，计划和尹hang 了解一下OAP项目，Dynamodb的需求。


释放端口 $ lsof -i :3000

3月8日
https://www.jenkins.io/zh/doc/tutorials/build-a-node-js-and-react-app-with-npm/
Standup meeting 
1 写完了admin项目CI/CD的代码，并做了测试，可以将dist路径下的所有文件deploy到S3，并且可以通过index.html的URL打开网页。

2 学习了一下DynamoDB以及通过Jenkins部署Springboot后端项目的相关的内容。

3 目前在配置JDK（Java Development Kit），Apache Maven等开发环境。


https://www.cnblogs.com/Chenjiabing/p/13953130.html


3 Dynamo EC2？ LMS部署？

ECS （Amazon Elastic Container Service）环境变量
ECR（Docker Image）上传
URL
AWS 


Dockerfile



java
JDK 15
gradle

https://segmentfault.com/a/1190000017208613



3月9日
Java SE Development Kit 15.0.2

git checkout -b OAP-7
ssh ec2-user@3.106.137.158
Standup meeting 
1 目前完成了admin项目CI/CD的代码，在UAT(user acceptance testing)部署和Production部署之间加了一个手工确认的步骤，也就是说在UAT部署，确认没有问题后，只有在点继续后才继续部署Production环境。 
昨天说的URL打不开页面的问题是bucket中ACL设置和允许static website hosting的问题。因为刚开始一直想着在代码中create buckect，所以每次部署都清空和删除原有buckect，然后重新创建一个同名的新的bucket，结果因为Everyone 的list和read权限，以及enable static website hosting 那里没法在代码中设置， 导致了上面说的问题。之后老板说bucket可以提前手动创建，所以上面的问题也就解决了。

Search 并学习一下，

2 昨天也和尹Hang讨论了一下OAP项目，包括Springboot项目的部署流程， Dokcer Image Repo, 也把尹Hang添加到了AWS的Developer用户组。

3 向Lunasol介绍了一下目前DevOps参与的项目，工作进展的程度；并且给介绍了我们在EC2上的Jenkins Server。


Loadbalancer
Logging

ELK

EKS: 确定不在EKS上做



分branch：
uat/branch/appname
staging
prod A
prod B
	数据库备份
MongoDB 的备份
Logging：UAT / Prod排错，7-30天
Montoring： Grafana，网站速度CISpeed，API，访问量
Cloudwatch：AWS

EKS


3月11日

1这两天我主要是按照老板开会的时候提的，我们的项目以后使用CI/CD的实际需求，把之前的，UAT部署和Prod部署放在一个pipeline的情况，分成了两个，一个来做Build，部署UAT，另一个部署Prod环境，并且做了一些验证和测试。昨天，我把我们项目的情况以及目前碰到的问题也和我们的老师聊了一下，他认为这样是可以的。

对于部署频度，UAT自动trigger每一次merge到master branch,自动build和部署；
Prod目前设置的是定期部署，比如每周六的0点，之后可以按照实际需求再修改，比如每2周一次甚至手动触发。

2另外，我设置了对不同的项目角色设置了不同的权限，比如普通developer只能看到UAT Job操作UAT的部署；
Senior developer 既能看见UAT也能看见Prod Job，也有权限操作Prod部署。

3计划今天研究一下，在有新的build产生的时候，能不能通过script来abort，来终止之前的build，这样可以节省EC2的资源占用。 以及在部署Prod之前加一些条件判断，以免。


git rebase master
git rebase --abort
git rebase --continue


AWS Lambda: AWS Lambda is a serverless compute service that lets you run code without provisioning or managing servers, creating workload-aware cluster scaling logic, maintaining event integrations, or managing runtimes. 


resource "aws_dynamodb_table" "dynamodb-terraform-state-lock" {
  name         = "terraform-state-lock-dynamodb"
  billing_mode = "PAY_PER_REQUEST"
  hash_key     = "LockID"
  attribute {
    name = "LockID"
    type = "S"
  }
}

https://bitbucket.org/jiang_ren/jr-admin.git

1 Moved Jenkinsfile from /jr-admin to /jr-admin/

https://www.jianshu.com/p/f1167e8850cd


3月15日
环境变量https://www.jenkins.io/doc/book/pipeline/jenkinsfile/#using-environment-variables

http://cicd.jiangren.com.au/env-vars.html/

可用环境变量列表
全局的自定义环境变量
设置了自定义的环境变量



最近主要是给CI/CD代码加入了一些内置环境变量以及设置了一些自定义环境变量。发现环境变量在Jenkinsfile中的使用比较麻烦，在代码中和shell script中用法都不太一样，$  } 单引号双引号都是有区分。

用admin项目测试，基本上是实现了部署到UAT和Prod的功能，提交PR给老板， 然后让老板测试一下，但是还有很多不完美的地方，计划逐步的优化。

stage("Env Variables") {
    steps {
         sh "printenv"
     }
}

+ printenv
GIT_PREVIOUS_SUCCESSFUL_COMMIT=3fc49859964b54838c9435150bf18d6a12b80667
NODE_VERSION=12.13.0
CI=true
HOSTNAME=87b793f76d86
RUN_CHANGES_DISPLAY_URL=http://3.106.137.158/job/jr-admin-uat/120/display/redirect?page=changes
YARN_VERSION=1.19.1
HUDSON_URL=http://3.106.137.158/
NODE_LABELS=master
GIT_COMMIT=687d9e6140ba77359019c4f4894035611758895b
HOME=/root
BUILD_URL=http://3.106.137.158/job/jr-admin-uat/120/
JENKINS_SERVER_COOKIE=durable-f14a8db5de3f509dc1b0613129caf138
WORKSPACE=/var/jenkins_home/workspace/jr-admin-uat
BUCKET_NAME=s3://uat-admin.jiangren.com.au
NODE_NAME=master
RUN_ARTIFACTS_DISPLAY_URL=http://3.106.137.158/job/jr-admin-uat/120/display/redirect?page=artifacts
GIT_BRANCH=origin/cicd-roger
EXECUTOR_NUMBER=1
STAGE_NAME=Env Variables
BUILD_DISPLAY_NAME=#120
RUN_TESTS_DISPLAY_URL=http://3.106.137.158/job/jr-admin-uat/120/display/redirect?page=tests
JOB_BASE_NAME=jr-admin-uat
HUDSON_HOME=/var/jenkins_home
PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
BUILD_ID=120
BUILD_TAG=jenkins-jr-admin-uat-120
JENKINS_URL=http://3.106.137.158/
GIT_URL=https://bitbucket.org/jiang_ren/jr-admin/
JOB_URL=http://3.106.137.158/job/jr-admin-uat/
BUILD_NUMBER=120
JR_ENVIRONMENT=UAT
JENKINS_NODE_COOKIE=b2b875e2-92dd-40b9-ad4d-957e92051b23
RUN_DISPLAY_URL=http://3.106.137.158/job/jr-admin-uat/120/display/redirect
HUDSON_SERVER_COOKIE=9252cf45e44ce774
JOB_DISPLAY_URL=http://3.106.137.158/job/jr-admin-uat/display/redirect
CLASSPATH=
JOB_NAME=jr-admin-uat
PWD=/var/jenkins_home/workspace/jr-admin-uat
GIT_PREVIOUS_COMMIT=3fc49859964b54838c9435150bf18d6a12b80667
WORKSPACE_TMP=/var/jenkins_home/workspace/jr-admin-uat@tmp


         // BRANCH_NAME == 'master' && CODE_CHANGES == true
         // anyOf {
         //   environment name: 'DEPLOY_TO', value: 'uat'
         //   environment name: 'DEPLOY_TO', value: 'production'
         // }

https://segmentfault.com/a/1190000038885050

indentation



系统管理 > 全局工具配置
JDK
配置本地 JDK 的路径，去掉勾选自动安装

Maven
配置本地maven的路径，去掉勾选自动安装
 
Build Tools:
Backend: Maven Gradle
Frontend/ Javascript: npm yarn
 
Configure Tools: Jenkins allow you to use tools
Jenkins will install automatically.
 
Install from Gradle.org
 
 
 
Package Tools
 
Check 
 
3月16日
1 昨天继续修改了一下admin项目CI/CD的代码，并把操作流程从头到尾给老板演示了一下，虽然实现了最最基本的UAT/prod部署功能，但还有问题，还会继续优化。然后也把代码从自己的branch，提交PR合并到了master branch. 针对老板提出的一些建议和功能，我们后续会逐步加进来。
2 admin项目前端部署积累的一些经验，也后续会用到OAP项目的前、后端CI/CD。查了些资料学习了一下Jenkins 构建和部署Gradle项目。
3 自己也复习了一下terraform创建EC2 和 DynamaDB。


GWT
Validat
验证
单元测试
Springboot部署的问题
CRUD
US改成AU
不能入眼



http://3.106.137.158:8080/bitbucket-hook/
http://cicd.jiangren.com.au/bitbucket-hook/


3月16日
在运行docker容器时可以加如下参数来保证每次docker服务重启后容器也自动重启：
docker run ****** --restart=always

如果已经启动了则可以使用如下命令：
docker update --restart=always <CONTAINER ID>


Standup meeting 
1 昨天主要做了些Jenkins Server的维护工作。发现最近并行build多,压力过大的话，container会自己stop. 
通过Cloudwatch调查了一下，除了CPU

给Jenkins cotainer设置了always restart，如果container stop后，可以自动restart，不需要SSH到EC2 手动重启。

内存 100  硬盘空间 超过50 挂载


2 另外，也协助John测试了一下，Jekins Server 发邮件的功能。


vol-03efcf7e81d0ec74a


codebuild 

code

查看EC2 EBS 使用量 $ df -hT /dev/xvda1



t3a.small 内存2Gib


Segmentation fault



+ docker build -f ./cicd/Dockerfile .
Sending build context to Docker daemon    252MB

Step 1/15 : FROM openjdk:15 AS build
 ---> 051805fe9464
Step 2/15 : WORKDIR /workspace/app
 ---> Using cache
 ---> d99fa7d1470f
Step 3/15 : COPY . /workspace/app
 ---> 6f68a95fac93
Step 4/15 : RUN chmod +x gradlew
 ---> Running in fb8f76dae8f5
Removing intermediate container fb8f76dae8f5
 ---> 5f2945fceb14
Step 5/15 : RUN ./gradlew clean build
 ---> Running in abe58d416f14
[91m./gradlew: line 39: cd: "./: No such file or directory
[0mDownloading https://services.gradle.org/distributions/gradle-6.8.2-bin.zip
..........10%..........20%..........30%...........40%..........50%..........60%..........70%...........80%..........90%..........100%

Welcome to Gradle 6.8.2!

Here are the highlights of this release:
 - Faster Kotlin DSL script compilation
 - Vendor selection for Java toolchains
 - Convenient execution of tasks in composite builds
 - Consistent dependency resolution

For more details see https://docs.gradle.org/6.8.2/release-notes.html

Starting a Gradle Daemon (subsequent builds will be faster)
> Task :clean UP-TO-DATE
> Task :compileJava
> Task :processResources
> Task :classes
> Task :bootJarMainClassName
> Task :bootJar
> Task :jar SKIPPED
> Task :assemble

> Task :compileTestJava
[91mNote: /workspace/app/src/test/java/com/jiangren/oap/repositories/CompanyRepositoryTest.java uses or overrides a deprecated API.
[0m[91mNote: Recompile with -Xlint:deprecation for details.
[0m
> Task :processTestResources
> Task :testClasses
> Task :test
Creating placeholder flownodes because failed loading originals.



3月29 

Standup meeting 
1 我继续调查了一下Jenkins Server 崩溃的情况，也做了些测试，发现的确与EBS Volume的剩余容量太小有关系，目前剩余3.8GB， 除了建的项目外，大量的plug-in也会占用一部分空间，Cloudwatch上关于EBS的指数突然变化的时间，和前天job build以及昨天压力测试的时间也是吻合的。也想跟老板商量一下，看咱们EBS再增大10G或20G?
100G 

NPM

2

3 另外也在考虑单EC2内，多一个容器的一个


OAP项目：
测试环境下
 


3月21日

安装Docker Compose
$ sudo curl -L "https://github.com/docker/compose/releases/download/1.25.0/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
$ sudo chmod +x /usr/local/bin/docker-compose


## 3月22日
































 














 















