MongoDB Atlas使用分享
=====================
## 什么是MongoDB?
MongoDB是一个NoSQL database,非常适用于startup的场景。

## 使用MongoDB的优势
* 简单好用：没有太多后端经验也可以轻松使用MongoDB
* dynamic schema: 在使用MongoDB时也可以很方便改变数据结构，特别是在前期业务不太明晰的时候是个很大的优势
* Horizontal：适合当业务量比较大的时候，MongoDB可以水平拓展
![avatar](https://tva1.sinaimg.cn/large/008i3skNgy1gv4nk2piqzj60mv0bnta802.jpg)

## 平时如何MongoDB
### MongoDB server： 
* community server
* enterprise server企业版
* MongoDB Atlas
    - 方便部署，不需要考虑太多配置问题

### 数据库和后端配合的方式：Monolithic架构 vs Atlas
#### Monolithic：数据库和后端都在一个ec2里

![avatar](https://tva1.sinaimg.cn/large/008i3skNgy1gv4o80r9ahj606m04kglg02.jpg)



优点：
* 试用与业务量小的时候，performance表现没有瓶径
* 成本小

#### Atlas：云托管的平台

![avatar](https://tva1.sinaimg.cn/large/008i3skNgy1gv4oh7zkwnj60c304it8l02.jpg)


优点：
* 配置简单
* 自动生成replica复制集，保证高可用性以及数据的backup
* 适合sharding水平拓展
* Easy to scale up and down
* 可以监看metric的实时指标
* 使用performance advisor工具
* 可靠的security setting


缺点
* 成本高
* Performance会出现瓶颈；如果达成和Monolithic部署方式相同的性能，成本更高

![altas_1](https://tva1.sinaimg.cn/large/008i3skNgy1gv4onp93dpj60ki0bb74r02.jpg)

![altas_2](https://tva1.sinaimg.cn/large/008i3skNgy1gv4omfdguwj60ms0bd75j02.jpg)

##### 什么是Replica set

![replica_set](https://tva1.sinaimg.cn/large/008i3skNgy1gv4oplemrqj60mi0bojrx02.jpg)

###### 原理
可以理解为起三个服务器。
如果从节点出现错误，会自动起一个从节点；
如果主节点出现错误，两个从节点的一个会选举一个作为主节点，然后一个新的备用节点产生，来保证高可用；
在主节点的配置上，也可以把Reads的权限给从节点，来减轻主节点的load。

##### Atlas配置步骤

![step1](https://tva1.sinaimg.cn/large/008i3skNgy1gv4orhcuwwj60mu0aqq3u02.jpg)

* Step 1: 创建一个项目
* Step 2: 创建一个新的集群

![step2](https://tva1.sinaimg.cn/large/008i3skNgy1gv4osoqzlwj60k70cvgmm02.jpg)

* Step 3: 选择服务提供商和区域，要和其他服务保持一致

![step3](https://tva1.sinaimg.cn/large/008i3skNgy1gv4otc7obcj60k80bswff02.jpg)

* Step 4: 选择连接方式，得到connect string, 将数据连接到Altas 

![step4](https://tva1.sinaimg.cn/large/008i3skNgy1gv4oup1htmj611y0emmye02.jpg)

![step5](https://tva1.sinaimg.cn/large/008i3skNgy1gv4ow51o61j611p0eldgw02.jpg)

* Step 5：设置Database和Network access 

当项目上线时，安全起见，ip地址要缩小范围，只适合某些服务器或者EC2

## 工作中使用的感受或者注意事项

### no index, no query
查询的field要配置上index。

比如，查询所有male的学生,确保male加了index；
或者叫所有leo的学生，first name要加index；
如果没有，要query整个表，性能马上下来，有很大的延迟。
例外：condition 1 and condition 2：
如果condition 1 已经把表缩到很小范围了，那么condition 2 就没有必要加了，因为加index也是有成本的。

### isDeleted要加index

进行软删除，因为分页要频繁操作

### Minimise the returned documents by projecting

### 避免过深的嵌套模式 
因为MongolDB每个文件小于16M；
把嵌套拆出来，把id引用起来。

### TTL保证数据库最小的size

