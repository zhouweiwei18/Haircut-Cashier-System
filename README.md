# 设计题目:基于springboot的收银系统的设计与实现

# 理发店收银系统功能概述
## _需求由来_
上网搜索了相关的资料，发现像超市、快餐店等这些实体店的收银系统有很多。理发店收银系统则较少，传统一些收银系统主要就是线下面对面方式的扫码支付，这样也很方便。不过像类似于理发店这种的实体店，这种方式可能并不是最好的。难道只有先到理发店理完发再结账这一种方式吗？不是的，我可以提前预约下单的方式啊，预约固定的理发时间，这样不是节省了很多时间嘛。举个例子来说，比如说今天要理发，也知道了要去哪家理发店，但不知道的是，这个时候理发店是否开门呢？店里面理发的人是否很多？理发师是否忙的过来吗？若是要排队的话，大概又要排多久呢？对于理发店而言不能够合理的为理发师安排顾客也是没有将资源最大化利用起来。这些是我们生活当中实实在在遇到的问题，其实解决这样的问题并不难，为此，我实现一套这样的系统来解决这些烦人的小问题!
## _我的解决方案_
我将我的想法先大致阐释一下，下面有具体的每个功能模块。顾客不一定都通过线下的方式，也可以通过线上的方式实时的掌握理发店里面的动态信息，还是以一位顾客要去理发的这个需求出发开始，可以提前下单预约理发时间。顾客在该理发店网上能实时查看该店的忙碌状态，并看到每一位理发师是否空闲，排队人数等信息从而为自己给出最优的预约时间。顾客选择相应理发师确定时间提前下单，这需要进行登录(短信接口)，可以选择支付方式微信、支付宝(支付接口)。预约完成后，顾客就可以看到自己的个人信息，这里面包括顾客最新的预约信息、会员服务(卡号、余额、充值按钮)、最近几次的消费记录、加入他们(相当于店家的招聘广告)等几样信息。下面用图例稍微解释下:

**1. 首先可以去该理发店网站看下当下店里面的忙碌状态，并选择自己想要的服务(比如说理发，洗头，烫头等)**

<img src="https://github.com/zhouweiwei18/Haircut-Cashier-System/blob/master/%E6%AF%95%E8%AE%BE%E5%9B%BE%E7%89%87%E7%B4%A0%E6%9D%90/%E9%97%A8%E5%BA%97%E5%AE%98%E7%BD%91.png" height="330px" width="480px" >
<img src="https://github.com/zhouweiwei18/Haircut-Cashier-System/blob/master/%E6%AF%95%E8%AE%BE%E5%9B%BE%E7%89%87%E7%B4%A0%E6%9D%90/%E5%BF%99%E7%A2%8C%E7%8A%B6%E6%80%81.png" height="330px" width="490px" >

***

**2.然后你可以选择你比较心怡的理发师进行下单预约**

<img src="https://github.com/zhouweiwei18/Haircut-Cashier-System/blob/master/%E6%AF%95%E8%AE%BE%E5%9B%BE%E7%89%87%E7%B4%A0%E6%9D%90/%E9%80%89%E6%8B%A9%E5%BF%83%E6%80%A1%E7%90%86%E5%8F%91%E5%B8%88.png" height="330px" width="480px" >

***

**3.未登录的状态下需要进行登录**

<img src="https://github.com/zhouweiwei18/Haircut-Cashier-System/blob/master/%E6%AF%95%E8%AE%BE%E5%9B%BE%E7%89%87%E7%B4%A0%E6%9D%90/%E7%99%BB%E5%BD%95.png" height="330px" width="480px" >

***

**4.扫码下单**

<img src="https://github.com/zhouweiwei18/Haircut-Cashier-System/blob/master/%E6%AF%95%E8%AE%BE%E5%9B%BE%E7%89%87%E7%B4%A0%E6%9D%90/%E6%94%AF%E4%BB%98.png" height="330px" width="480px" >

***

**5.下单完成后，就可以知道自己预约以及相关信息**

<img src="https://github.com/zhouweiwei18/Haircut-Cashier-System/blob/master/%E6%AF%95%E8%AE%BE%E5%9B%BE%E7%89%87%E7%B4%A0%E6%9D%90/%E6%9C%80%E6%96%B0%E9%A2%84%E7%BA%A6.png" height="330px" width="480px" >
<img src="https://github.com/zhouweiwei18/Haircut-Cashier-System/blob/master/%E6%AF%95%E8%AE%BE%E5%9B%BE%E7%89%87%E7%B4%A0%E6%9D%90/%E6%B6%88%E8%B4%B9%E8%AE%B0%E5%BD%95.png" height="330px" width="480px" >
<img src="https://github.com/zhouweiwei18/Haircut-Cashier-System/blob/master/%E6%AF%95%E8%AE%BE%E5%9B%BE%E7%89%87%E7%B4%A0%E6%9D%90/%E4%BC%9A%E5%91%98.png" height="330px" width="480px" >
<img src="https://github.com/zhouweiwei18/Haircut-Cashier-System/blob/master/%E6%AF%95%E8%AE%BE%E5%9B%BE%E7%89%87%E7%B4%A0%E6%9D%90/%E6%89%BE%E5%B7%A5%E4%BD%9C.png" height="330px" width="480px" >

***

## 简要说下后台管理模块 

### _消费管理_
说明: 主要的结账功能模块，前台结账
* 线下消费：
> 也就是直接到店理发的顾客，没有网上预约，此时需要收银员手动创建该顾客的订单(指明理发师--关系到理发师的工资)。 
* 线上消费: 
> 顾客通过网上预约的方式来店里的，这个时候收银员可以将订单状态修改为已完成即可，或者说系统自动在某时刻默认修改。
> 这里也可以有理发师来为顾客结账，顺便帮顾客查看余额信息等其它的信息
* 消费明细: 
> 也就是理发店每项服务的价格明细:理发:30，烫头：300.....

### _(理发师) 员工管理_
* 招募员工: 
> 员工来源于顾客(顾客可以申请职位)，也可以手动添加。只有管理员有权限
* 修改员工信息：
> 涨基本工资(根据理发师被预约的次数和线下为顾客服务次数综合考虑)、员工状态(辞职，在班，外出学习...)
* 管理员: 
> 只有管理员可以使用(超级管理员--管理--管理员)

### _(消费者) 顾客管理_
* 新增顾客: 
> 前台顾客会自动登录添加自己的信息(默认非会员) (线下消费者  当要开发票的时候)，若是新增会员用户可以由收银员手动添加
* 修改顾客信息:
> 基本字段修改啥的，为顾客开通会员啥的
* 顾客查询：
> 能够快速查找到某一用户(模糊查询)
* 会员充值：
> 收银员通过输入用户手机号进行搜索(用户名也行) 用于线下充值(面对面付钱)

### _统计报表_
* 收支汇总: 
> 也就是这个总的收入明细(收入:顾客消费(订单)   支出:员工工资、奖金、租金等) 可以按月份查询、显示内容
* 工资统计: 
> 平均工资，各员工月工资涨幅等  按月份查询、显示内容
* 消费统计: 
> 有会员消费、续费、线上消费、线下消费等统计

### _系统维护_
* 网站首页: 
> 首页的轮播图更换(广告，招聘信息等啥的)


***

## 简要通过图例说明下:
1. **后台首页**
> 若要仅仅进入系统的浏览，无需登录，可立即使用(游客)。若是要对数据操作啥的，需要管理员权限(一般管理员:员工  超级管理员:老板)
<img src="https://github.com/zhouweiwei18/Haircut-Cashier-System/blob/master/%E6%AF%95%E8%AE%BE%E5%9B%BE%E7%89%87%E7%B4%A0%E6%9D%90/%E5%90%8E%E5%8F%B0%E9%A6%96%E9%A1%B5.png" height="330px" width="480px" >
<img src="https://github.com/zhouweiwei18/Haircut-Cashier-System/blob/master/%E6%AF%95%E8%AE%BE%E5%9B%BE%E7%89%87%E7%B4%A0%E6%9D%90/%E7%AE%A1%E7%90%86%E5%91%98%E7%99%BB%E5%BD%95.png" height="330px" width="480px" >


***

2. **后台的管理页面**
<img src="https://github.com/zhouweiwei18/Haircut-Cashier-System/blob/master/%E6%AF%95%E8%AE%BE%E5%9B%BE%E7%89%87%E7%B4%A0%E6%9D%90/%E7%AE%A1%E7%90%86%E9%A1%B5%E9%9D%A2.png" height="500px" width="900px" >

3. **给预约用户结账**
<img src="https://github.com/zhouweiwei18/Haircut-Cashier-System/blob/master/%E6%AF%95%E8%AE%BE%E5%9B%BE%E7%89%87%E7%B4%A0%E6%9D%90/%E7%90%86%E5%8F%91%E5%B8%88%E7%BB%93%E8%B4%A6.png" height="330px" width="480px" >
<img src="https://github.com/zhouweiwei18/Haircut-Cashier-System/blob/master/%E6%AF%95%E8%AE%BE%E5%9B%BE%E7%89%87%E7%B4%A0%E6%9D%90/%E9%A1%BE%E5%AE%A2%E6%B6%88%E8%B4%B9%E5%88%97%E8%A1%A8.png" height="330px" width="480px" >

4. **生成订单**
<img src="https://github.com/zhouweiwei18/Haircut-Cashier-System/blob/master/%E6%AF%95%E8%AE%BE%E5%9B%BE%E7%89%87%E7%B4%A0%E6%9D%90/%E8%AE%A2%E5%8D%95.png" height="330px" width="480px" >

5. **线下消费**
<img src="https://github.com/zhouweiwei18/Haircut-Cashier-System/blob/master/%E6%AF%95%E8%AE%BE%E5%9B%BE%E7%89%87%E7%B4%A0%E6%9D%90/%E7%BA%BF%E4%B8%8B%E6%B6%88%E8%B4%B9.png" height="330px" width="480px" >

## _需要用到的技术_
* SpringBoot + Mybatis
* Shiro 权限管理
* 第三方接口接入: `短信接口接入`,`扫码支付接口`,`第三方登录:QQ互联`...
* 数据库 : MySQL数据库
* Linux服务器



