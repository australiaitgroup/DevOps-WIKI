# 课堂笔记

## 1.自我介绍
Holly Liu:  DevOps Consultant at Versent  
有做过公开课，可以在jiangren youtube找，

课程讲解以亚马逊云平台为主
DevOps所需要的工具和配置，将在下次tutorial讲解

### Class Rules
- Turn on your camera
  - 可以开camera，让老师同学记住你
- Do the handson
  - 要hands on，无论上课演示的，还是课下的，都要自己做一遍，跟下来
- You’ll do the troubleshooting
  - 首先，如果有问题，你的error message/code
  - 然后看到error之后，你要想到自己的做法，你的trouble shooting step是什么
  - 大部分问题，是可以google解决的
- Raise questions at any time
  - 随时提问，任何形式都欢迎

### DevOps怎么去学习
- 不断去学习，不断去迭代，不断去巩固自己的知识

## 2.Case study: optimising jiangren.com.au
### Scenario
Jiangren company has a website called “http://jiangren.com.au”. It’s intended for Australian customers. Since the company is expanding its global market, the CEO wants to improve its website with low latency and high availability to global customers. 
Your task is to find out what are the current problems, what solution and how to implement it. 

### 关键词提取
由上面的描述可取出关键词：
- Low latency
- High availability
  - 希望各地区用户都能正常的访问业务，既使在某一个区收到影响的情况下

### 分析问题
#### Latency
如果网页load速度慢10～20%，traffic会受到致命打击
##### Latency/网站访问测速
https://www.dotcom-tools.com/website-speed-test.asp
- 1. 打开以上链接在三个不同的tab里，测三次，取平均值
- 2. Location取aws在世界各地的data centre附近地区
  - Denver, N.Virginia, Frankfurt, Tokyo, Brisbane
  - 第二次可以选取不同地区的不同城市
- 3. 选择Global Perfermance
#### 测速结果分析
网站仅针对了澳洲顾客服务，还没有对全球顾客进行优化，需要对Global Latency做优化  
As shown above, Jiangren.com.au loads as fast as 2.6 seconds in Brisbane. However, it takes a few times to load in other locations.

#### Availability
看一下这个网站有几个不同的server
##### DNS/网站服务器数量测试
- Online Tools
  - DNS Check
    - https://www.whatsmydns.net
    - 可以检测该网站在全球不同地区访问时，对应的ip address
    - 作为优化，一个网站如果在全球有edge location的话，里面可以帮忙缓存网站的内容，这样可以用户访问，将首先到达最近的edge location，大幅提高访问速度
  - IP Check
- Cmds
  - mac/linux: dig
  - windows: nslookup 
   
#### DNS测试结果分析
网站没有对全球访问做优化，仅有一个ip/server来应对全球访问
- 这个架构我们叫做Single Point Failure   
  
There is only one EC2 node for the jiangren.com.au website. If there is the EC2 node is failed, then the website will be inaccessible.
If there is a spamming user sends a significant amount of request or use DDoS to attack the server, then the server will be overloaded and out of service.
- DDoS Attack
  - 黑客可以控制大量全球不同的服务器，来同时访问你的网站，超过网站的负载量，来阻断其它/真实用户的访问
 

### 解决方案
#### Content Delivery Network (CDN)
帮助你把文件储存在全球不同的地区，在不同大陆设置不同的edge server，可以便于用户访问时，直接到达该地区的edge server，拿到网站的缓存，以达到快速访问
- Akamai: CDN的一个品牌，帮你设置多个edge server
- 用户访问时，如果离该地最近的edge/cache server挂掉，那么用户会访问到其它的edge/cache server，或直接访问origin server 

##### What CDN can help you 
- Improve page load speed
- Handle high traffic loads
  - 通过分摊对主服务器的访问给edge server，来缓解主服务器的压力
- Reduce bandwidth consumption
- Load balance between multiple servers
- Protect your website from DDoS attacks
- Secure your application
- And more

##### CDN on AWS: CloudFront(Handson)
- Setup: https://github.com/JiangRenDevOps/DevOpsLectureNotesV4/blob/main/WK1-CDN-DNS/CDN.md
- 对应课程视频1:12:30 ~ 1:38:10

##### Summarise CDN
并没有改变任何jiangren.com.au的设置和部署，只是新建了一个global distribution，来提升jiangren的各项指标  
CDN works well with static resources. We didn’t cover cache settings for backend REST API calls. You can exclude backend calls so they won’t be cached by CDN.  

Pros
- High Speed: Reduce web page load time
- High Availability: Reduce requests from original server and prevent DDoS attack
 
Cons
- Additional сosts
  - https://aws.amazon.com/cloudfront/pricing/
  - CloudFront里，`Edit Distribution`- `Distributon Settings`里可以设置`Price Class`来限制CDN部署的区域
- Application needs to cdnify via file versioning. Otherwise, files takes time
to update.
  - cache server可能没有拿到网站的最新版本，同步还没有进行到

#### Domain Name Server(DNS) 
![dns intro](image/c0201.png)
- 在敲入网址后，系统会在浏览器的缓存里，寻找有没有储存相关的IP address
- 在没有找到相对应的ip后，会继续访问ISP（e.g. Telstra, Optus）, 找到对应ip
- 如果没还有找到，可能会去询问更高层的domain name server，例如root/TLD/authoritative name server
  - TLD name server，包含了所有的以.com或者.net结尾的网站对应ip信息
- If you search “Domain name registration”, you will find a lot of providers. My favourite ones are:
  - godaddy.com
  - onlydomains.com 
  - namecheap.com 
  - freedns.afraid.org（免费的）
- For DNS hosting, we use Route53 in AWS. In this course, we are going to use AWS Route53 to demo the DNS setup for our CDN

##### DNS: AWS Route53(Handson)
![jiangren dns](image/c0202.png)
并不会直接使用jiangren.com.au，而是使用了一个subdomain
可以在AWS console页面，search栏搜索route 53进入
- Setup: https://github.com/JiangRenDevOps/DevOpsLectureNotesV4/blob/main/WK1-CDN-DNS/DNS.md
- 对应课程视频2:03:20 ~ 2:26:00
- (AWS) CNAME:将现有record的名字，map到另一个域名（例如cloudfront里产生的新域名）或者subdomain
- 有方法将cloudfront.net从客户端禁用：https://stackoverflow.com/questions/45589416/how-to-disable-access-to-cloudfront-via-the-cloudfront-net-url
- 子域名必须要与主域名有关系（例如已经保存在了aws hosted zone里），才能使我们的网站得到最终的访问。因为一般在访问子域名时，会向上追溯到主域名，在主域名dns处询问是否有相应的子域名，如果得到了否定回答，则子域名依然无法访问

##### DNS Records on Route53
每次我们创建一个hosted zone时，都会自带两个records(并不需要我们去更改)：
- NS: Name Server
- SOA: Start of Authority

## 4.Homework
https://github.com/JiangRenDevOps/DevOpsLectureNotesV4/blob/main/WK1-CDN-DNS /homework.md

## 5.AWS
- 市场龙头地位
- 这学期我们会贯穿学习有关AWS的各类知识
- 历史：
  - 早期是amazon的内部工具
  - 发展至今，已经形成了一个很大的版图：
![aws services](image/c0203.png)
- 开始接触最多的是EC2(虚拟机业务)
- 这个图基本上是我们最常用的
- 关于考证：
  - 非常鼓励大家去考取
  - DevOps 就业领域也有很大的缺口，同时对Junior也有很友好的培养
  - 注册：https://www.aws.training/SignIn?returnUrl=%2FDetails%2FeLearning%3Fid%3D20686
  - Michael老师的备考笔记：https://github.com/michaelsu2014/aws-solution-architect-associate-notes

## 6.In Class Handson
### CloudFront(CDN) Setup:
https://github.com/JiangRenDevOps/DevOpsLectureNotesV4/blob/main/WK1-CDN-DNS/CDN.md

### AWS Route53 Setup:
https://github.com/JiangRenDevOps/DevOpsLectureNotesV4/blob/main/WK1-CDN-DNS/DNS.md
