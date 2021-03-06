# 学员模块
看到自己的缴费清单, 选择清单中某项进行缴费操作
+ 登陆(注册由校方批量注册,然后告知学员账号密码)
+ 查询缴费清单
+ 线上缴费
+ 微信缴费

# 教师模块
+ 学员信息
    + 新建
    + 批量新建(导入文件)
    + 搜索,修改
+ 缴费项目维护
    + 新建
    + 修改
    + 删除
+ 缴费清单(要使用滞纳金规则)
    + 缴费统计
    + 新建缴费清单
    + 批量新建(导入)
    + 线下缴费
+ 自动催缴
    + 设置规则,对所有的
+ 滞纳金管理
    + 设置滞纳金规则
+ 现金缴费(作为一个附加缴费项目,附加到一个缴费清单中,实现相应的缴费清单金额的减免.)
    + 搜索指定学员的缴费清单,然后添加附加缴费项目(现金缴费)到清单中, 等待财务审核通过后, 该现金项目正式的加入到相应清单中.
    + 清单说明里面,可以提, 该清单已经线下缴款1000元, 请在线上缴纳剩余部分的钱.
    + 如果线下全部缴纳完毕, 在财务审核后,就可以标记为已经缴纳.


# 财务模块 (和尚德模块一样,就不设计了)
+ 注册/登陆
+ 科目维护
+ 现金收款
+ 日终处理
+ 对账
+ 财务报表




# 实体

## 缴费项目
+ 缴费项目编码(JF000001)
+ 缴费项目名称(缴费项目的名称.如:2016年春季学费)
+ 缴费项目金额(要缴纳的金钱数)
+ 缴费项目类型(主缴费项目和附加缴费项目及减免项目)
+ 缴费项目描述(说明资金的收取原因)

example:
+ 编码:ZJF0001
+ 名称:2016年春游
+ 金额:200
+ 类型: 主缴费项目
+ 描述: 用于春游的个人花费

+ 编码:FJF0001
+ 名称:2016年春游捐款
+ 金额:100
+ 类型:附加缴费项目(可选)
+ 描述:2016年春游时为当地贫困人员捐款

+ 编号:JJF0001
+ 名称:通用减免
+ 金额:-100,
+ 类型:主收费项目
+ 描述:对部分学员进行费用减免的项目.

## 学员
+ 学号
+ 密码
+ 学员姓名
+ 性别
+ 学员手机号
example:
+ XH0001
+ 123456
+ 五月花
+ 18649111230

+ XH0002
+ 123456
+ 六月雪
+ 186392475865

## 缴费清单(必须有主缴费项目)---可以从该清单中,产生多个订单(Order)
+ 清单编号
+ 清单名称
<!--+ 缴费项目编号(一个列表,多个缴费项目,主要是主附缴费项目, 特殊情况会添加优惠缴费项目对整体清单的金额进行减免(比如完成了部分线下缴费))-->
+ 描述:(用于描述该缴费清单的收款原因)
<!--+ 现金缴纳部分金额:-->
+ 滞纳金规则:(用于该缴费清单的滞纳金规则)
+ 截止时间(请在截止时间前缴费,否则会根据滞纳金规则计算滞纳金).
<!--+ 已缴人数(显示)-->



## 清单,人员关系表(存储一个清单中有哪些的关联人员)
+ 唯一id
+ 人员编号
+ 清单编号
+ 缴费项目[](在同一个缴费清单中,处理大家都一样的拥有清单上的缴费项目信息, 还有一些个人的减免项目的个性化信息.)
+ 状态(表示该人员是否已经完成该清单的缴费)
+ 以缴金额(该人员所有项目合计的缴纳金额)

## 清单,项目关系表(一个清单的关联项目)
+ 唯一id
+ 订单编号(在该表中不唯一)
+ 物品编号
<!--+ 数量(0:不缴纳, 1:缴纳一份, -1:减免, n:)-->
<!--+ 物品单价-->
<!--+ 物品其他关键信息(从项目中以json字符串格式提取出来)-->

example:
+ 清单编号:QD0001
+ 清单名称:2016春游费用
+ 应缴人员编号:XH0001
+ 缴费项目编号:[ZJF0001, FJF0001]
