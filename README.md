# 中国飞行者联盟活动管理中心辅助软件V1.1

# 用户手册

欢迎使用中国飞行者联盟活动管理中心辅助软件V1.1，下面将为用户介绍本软件的使用

**Author:** 
	Gavin Gao (CFR2493)
**Open Source License Agreement:**
	MIT license, Copyright © 2024 Gavin Gao



### 更新日志

- **V1.1**

​	新增Event Publish(活动发布)页面
​	新增log自动记录功能
​	新增从日志文件导出机组功能
​	新增以机场ICAO代码为名称的检查点经纬度坐标自动填充功能
​	进一步优化机组导出功能，将多文件方式修改为单文件多工作表方式
​	将源代码开源至Github

- **V1.0**

  软件的第一个版本，初步完成了ATC Online与Aircraft Detect功能

### ATC Online

ATC Online页面可供用户导出在线管制员名单	<img src="C:\Users\Gavin Gao\AppData\Roaming\Typora\typora-user-images\image-20240310213257355.png" alt="image-20240310213257355" style="zoom: 80%;" />

首先，添加起飞机场与落地机场。注意，此处的起飞机场与落地机场可以填写多条，若填写错误，可以双击错误项删除。
添加完成后，即可点击导出按钮，此时便会将当前时刻在线的管制员按照用户设置的起飞落地机场分类后显示在Excel文档中。

### Aircraft Detect

Aircraft Detect页面可供用户导出机组列表	<img src="C:\Users\Gavin Gao\AppData\Roaming\Typora\typora-user-images\image-20240310214051605.png" alt="image-20240310214051605" style="zoom:80%;" />

导出机组列表的逻辑如下：

- 每一个检查点独立判断，只记录经过本检查点附近，满足垂直高度与水平高度要求的机组
- 最终导出Excel文件时，会为每一个检查点单独创建一个工作表，可由用户自主切换
- 点击开始检测后，程序即自动定时从服务器下载数据，并根据用户填写的各个检查点信息，判断在各个检查点附近的机组，满足水平与垂直高度要求，即记录至程序内部。当用户不需要继续检测时（如联飞活动已结束），即可点击结束检测，再点击导出数据，即可将机组数据导出为Excel表格
- 开始检测前，必须保证至少添加了一个检查点信息，不同检查点之间名称不能重复，否则将会以新纪录覆盖原有记录（也就是修改检查点信息）。如果用户需要删除检查点，在检查点列表中找到对应项目，双击即可删除
- 开始检测后，用户无法再修改检查点信息，直至结束检测为止
- 一次检测结束后，用户应根据需要及时导出机组数据。若未导出，在下一次开始检测时，会将原有机组数据覆盖
- 本软件在开始检测后，会自动记录日志文件，并存放在与软件同级的名为Output的文件夹内，文件名称为开始检测的时间戳，扩展名为log
- 由于各种原因，用户无法或者不能及时导出数据，可以下次择期进入软件，正确设置检查点信息后，点击从日志文件中导出，并选择对应的日志文件，即可重新导出原有数据
- 部分版本支持识别以机场ICAO代码为名称的检查点，若用户在检查点处输入ICAO代码，当用户点击其他位置后，部分机场可自动识别并填写其经纬度坐标，便于用户使用
- 最低高度与最高高度单位为英尺(feet)。若留空，最低高度默认值为0英尺，最高高度默认值为48900英尺，即在此高度范围内的机组才会纳入统计范畴
- 水平范围单位为千米(km)，且该项不可为空，即机组在以检查点为圆心，水平范围为半径的圆内才会被纳入统计范畴
- 机组只有在上述的水平与垂直范围内，即同时满足水平与垂直范围，才会纳入统计范畴，否则将自动忽略

### Event Publish

Event Publish页面可供中国飞行者联盟活动管理中心成员自动登录活动发布账号，并自动进入活动发布界面

**特别注意：只有内部发布版本的软件，自带账号密码且可自动登录，对外发布的软件仍需手动登录网页。各位活动管理员注意安全以及隐私保护，严防泄密事件发生**

由于Event Publish页面需要调用Chromium内核，这导致整个软件体积极大。在接下来的版本中，可能会考虑取消这一页面或采用其他合理方式替代之。
