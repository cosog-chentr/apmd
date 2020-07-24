:link:[**数据库文档**](./database/):link:

# 《敏捷生产V7.3》用户手册

- [第一章 系统介绍](#第一章系统介绍)
    - [1.1 环境要求](#1.1环境要求)
    - [1.2 驱动说明](#1.2驱动说明)
    - [1.3 系统使用说明](#1.3系统使用说明)
	- [1.4 工况说明](#1.4工况说明)
      - [1.4.1 平衡工况](#1.4.1平衡工况)
      - [1.4.2 功图工况](#1.4.2功图工况) 
- [第二章 应用介绍](#第二章应用介绍) 
    - [2.1 页面布局](#2.1页面布局)
    - [2.2 实时评价](#2.2实时评价)
      - [2.2.1 统计](#2.2.1统计)
      - [2.2.2 目标井](#2.2.2目标井)
      - [2.2.3 单井数据](#2.2.3单井数据)
    - [2.3 全天评价](#2.3全天评价)
    - [2.4 生产报表](#2.4生产报表)
    - [2.5 图形查询](#2.5图形查询)
    - [2.6 权限管理](#2.6权限管理)
      - [2.6.1 单位管理](#2.6.1单位管理)
      - [2.6.2 用户管理](#2.6.2用户管理)  
    - [2.7 数据配置](#2.7数据配置)  
      - [2.7.1 井名信息](#2.7.1井名信息)  
      - [2.7.2 生产数据](#2.7.2生产数据)
      - [2.7.3 井身轨迹](#2.7.3井身轨迹)
      - [2.7.4 抽油机信息](#2.7.4抽油机信息) 
      - [2.7.5 驱动配置](#2.7.5驱动配置)  
      - [2.7.6 计算维护](#2.7.6计算维护) 
    - [2.8 系统配置](#2.8系统配置)  
      - [2.8.1 字典配置](#2.8.1字典配置) 
      - [2.8.2 统计配置](#2.8.2统计配置) 
      - [2.8.3 报警配置](#2.8.3报警配置) 
- [附件1 数字化抽油机](#附件1数字化抽油机)
    - [F1.1 智能机柜操作说明](#F1.1智能机柜操作说明)
    - [F1.2 自动调节控制流程](#F1.2自动调节控制流程)
    - [F1.3 平衡度判断方法](#F1.3平衡度判断方法)
    - [F1.4 操作项含义](#F1.4操作项含义) 
    - [F1.5 曲柄平衡移动距离](#F1.5曲柄平衡移动距离)
    - [F1.6 电参工况](#F1.6电参工况)

<h1><a name="第一章系统介绍"></a>第一章 系统介绍</h1>  

<h2><a name="1.1环境要求"></a>1.1 环境要求</h2>

**1.Web服务器**  
>- CPU：2核及以上  
>- 内存：8G及以上  
>- 硬盘：500G及以上  
>- 操作系统：建议Windows server 2012 64位及以上  
>- 数据库：Oracle 11g及以上  
>- JDK：8.0及以上  
>- Tomcat：9.0及以上

**2.云计算服务器**

>- CPU：2核及以上  
>- 内存：8G及以上  
>- 硬盘：80G及以上  
>- 操作系统：建议Ubuntu server 16.04及以上

<h2><a name="1.2驱动说明"></a>1.2 驱动说明</h2>

**1.中石油标准**  
&emsp;&emsp;支持中石油A11标准及拓展驱动  
**2.中石化标准**  
&emsp;&emsp;支持中石化“四化”标准及拓展驱动  
**3.边云结合**  
&emsp;&emsp;支持MQTT、kafka订阅模式协议

<h2><a name="1.3系统使用说明"></a>1.3 系统使用说明</h2>  

&emsp;&emsp;系统部署完成后需要根据使用者实际情况进行数据配置，流程如下：  
>1. 输入默认的系统管理员账号进入系统；  
>2. “单位管理”模块创建单位信息，**详情查看2.6.1节**；  
>3. “用户管理”模块为单位创建用户，**详情查看2.6.2节**；  
>4. “井名信息”模块录入井信息，**详情查看2.7.1节**；录入完成后，可在界面查看前端设备采集的数据（包括功图、离散数据等），如果是数字化抽油机，可进行调节平衡工作；  
>5. “生产数据”模块录入井的油层数据、泵数据、杆柱组合数据等，**详情查看2.7.2节**；录入完成后，可进行功图工况诊断和产量计算，得到功图工况、产量、泵效、杆柱应力、系统效率、物性剖面等计算分析结果； 
>6. “井身轨迹”模块录入井的测量深度、井斜角、方位角，**详情查看2.7.3节**；录入完成后，可在界面中画出井身轨迹图；  
>7. “抽油机数据”模块录入抽油机相关数据；录入完成后，可进行曲柄平衡计算，得到曲柄平衡块移动距离、目前/预期扭矩曲线（包括载荷扭矩、平衡块扭矩、曲柄扭矩、净扭矩）及抽油机运动特性曲线（包括位移、速度）；  
>8. 前端传感器采集传输完成后，可在界面查看相关结果。  

<h2><a name="1.4工况说明"></a>1.4 工况介绍</h2>  

<h3><a name="1.4.1平衡工况"></a>1.4.1 平衡工况</h3>  

&emsp;&emsp;范围可根据实际情况在“统计配置”模块电流平衡、功率平衡选项中修改。  

| **序号** | **范围**           | **名称**       |
|----------|--------------------|----------------|
|1         | 平衡度＜70%        | 严重欠平衡     |
|2         | 70%＜平衡度≤85%    | 欠平衡         |
|3         | 85%＜平衡度≤100%   | 平衡           |
|4         | 100%＜平衡度≤115%  | 过平衡         |
|5         | 115%＜平衡度       | 严重过平衡     |

<h3><a name="1.4.2功图工况"></a>1.4.2 功图工况</h3>
  
| **序号** | **代码** | **名称** | **优化建议** |
|----|------|------------------|-------------|
| 1  | 1201 | 抽喷             |             |
| 2  | 1203 | 充满不足         |              |
| 3  | 1204 | 供液不足         | 间抽或降低冲次 |
| 4  | 1205 | 供液极差         | 间抽或降低冲次 |
| 5  | 1206 | 抽空             | 间抽或降低冲次 |
| 6  | 1207 | 泵堵             | 热洗或加药 |
| 7  | 1208 | 气锁             | 合理控制气体 |
| 8  | 1209 | 气影响           | 合理控制气体 |
| 9  | 1210 | 间隙漏           | 检泵 |
| 10 | 1211 | 油管漏           | 油管打压试验 |
| 11 | 1212 | 游动凡尔漏失      | 热洗或检泵 |
| 12 | 1213 | 固定凡尔漏失      | 热洗或检泵 |
| 13 | 1214 | 双凡尔漏失        | 热洗或检泵 |
| 14 | 1215 | 游动凡尔失灵      | 检泵 |
| 15 | 1216 | 固定凡尔失灵      | 检泵 |
| 16 | 1217 | 双凡尔失灵        | 检泵 |
| 17 | 1218 | 上死点别、碰      | 校正井口设备 |
| 18 | 1219 | 碰泵             | 上提（增大）防冲距 |
| 19 | 1220 | 柱塞未下入工作筒   | 下放（缩小）防冲距 |
| 20 | 1221 | 柱塞脱出工作筒    | 下放（缩小）防冲距 |
| 21 | 1222 | 杆断脱           | 替换抽油杆 |
| 22 | 1223 | 杆（泵）卡        | 热洗或检泵 |
| 23 | 1224 | 轻微结蜡          | 热洗或加药 |
| 24 | 1225 | 严重结蜡          | 热洗或加药 |
| 25 | 1226 | 轻微出砂          | 防砂      |
| 26 | 1227 | 严重出砂          | 防砂      |
| 27 | 1230 | 惯性载荷大        | 降低冲次    |
| 28 | 1231 | 应力超标          | 优化抽油杆柱组合 |
| 29 | 1232 | 采集异常          | 检查采集仪表 |
| 30 | 1302 | 停抽             |           |
| 31 | 1202 | 正常             |           |  

<h1><a name="第二章应用介绍"></a>第二章 应用介绍</h1>

&emsp;&emsp;**浏览器要求：建议谷歌浏览器、360浏览器极速模式、IE9以上版本**

<h2><a name="2.1页面布局"></a>2.1 页面布局</h2>

>1. banner区：包括修改密码、退出、帮助及全屏按钮；  
>2. 功能导航区：系统各主功能模块；  
>3. 组织导航区：用户组织结构；  
>4. 统计区：井信息统计图表；  
>5. 单井数据区：单井分析、采集及控制详细信息。

&emsp;&emsp;通过点击界面中缝位置的图标![伸缩按钮](../images/helpdoc/PNG/025.png?raw=true)或![伸缩按钮](../images/helpdoc/PNG/026.png?raw=true)可实现界面伸缩。

![列表伸缩](../images/helpdoc/PNG/001.png?raw=true)

<h2><a name="2.2实时评价"></a>2.2 实时评价</h2>

&emsp;&emsp;根据油井的动静态数据对单井进行实时评价。**有新数据时（包括功图和离散数据），界面自动刷新。**

<h3><a name="2.2.1统计"></a>2.2.1 统计</h3>

>1. 统计主标签：包括功图工况、电参工况、产量、平衡、时率、效率、电量、通信；  
>2. 统计子标签：各主标签包含的子项，如平衡包括电流平衡和功率平衡；  
>3. 统计表/图：根据选择的主标签、子标签显示相关统计信息。

![统计](../images/helpdoc/PNG/004.png?raw=true)

<h3><a name="2.2.2目标井"></a>2.2.2 目标井</h3>

&emsp;&emsp;如需查看某一类目标井的具体信息时，例如采集异常，  
>1. 点击统计图中“采集异常”对应的饼或标签；  
>2. 统计表中显示该组织下的所有“采集异常”井；  
>3. 右侧单井详情中显示该井的详细信息；  
>4. 选择一行后点击**单井历史**或**双击**该行可查看该井的历史信息。

![目标井](../images/helpdoc/PNG/005.png?raw=true)

<h3><a name="2.2.3单井数据"></a>2.2.3 单井数据</h3>

&emsp;&emsp;包括图形及分析、采集、控制。

![单井数据](../images/helpdoc/PNG/006.png?raw=true)

#### 2.2.3.1 图形  

**1. 井筒分析**  

**（1）光杆功图**  
>- 功图采集时间  
例如：2020-06-08 10:18:24  
>- 上理论载荷线  
上理论载荷=活塞以上液柱载荷+抽油杆在液柱中的载荷  
>- 下理论载荷线  
下理论载荷=抽油杆在液柱中的载荷  
>- 最大载荷  
功图最大载荷  
>- 最小载荷  
功图最小载荷  

![光杆功图](../images/helpdoc/PNG/027.png?raw=true) 

**（2） 泵功图**  
&emsp;&emsp;从上至下依次为：  
>- 地面功图  
>- 二级杆顶端功图  
>- 泵功图  

![泵功图](../images/helpdoc/PNG/028.png?raw=true)

**（3） 杆柱应力**  
&emsp;&emsp;根据杆柱组合，分析各级杆柱的受力情况，判断杆柱组合是否合理。  
>- 一级杆顶端应力百分比  
>- 二级杆顶端应力百分比  
>- 应力百分比=最大应力/许用应力  

![杆柱应力](../images/helpdoc/PNG/029.png?raw=true)

**（4） 泵效组成**  
&emsp;&emsp;泵的实际排量与泵的理论排量之比的百分数称为泵效。

![泵效组成](../images/helpdoc/PNG/030.png?raw=true)

**（5） 物性剖面**  

![物性剖面](../images/helpdoc/PNG/031.png?raw=true)

**（6） 井身轨迹**  

![井身轨迹](../images/helpdoc/PNG/032.png?raw=true)

**2. 地面分析**

**（1） 电功图**  
&emsp;&emsp;电功图是电的有功功率图，功率平衡度计算：  
&emsp;&emsp;功率平衡度=下冲程有功功率最大值/上冲程有功功率最大值  

![电功图](../images/helpdoc/PNG/034.png?raw=true) 

**（2） 电流图**  
&emsp;&emsp;电流平衡度计算：  
&emsp;&emsp;电流平衡度=下冲程电流最大值/上冲程电流最大值  

![电流图](../images/helpdoc/PNG/035.png?raw=true)

**（3） 三相电流曲线**  

![三相电流曲线](../images/helpdoc/PNG/036.png?raw=true)  

**（4） 目前扭矩曲线**  

![目前扭矩曲线](../images/helpdoc/PNG/037.png?raw=true)

**（5） 预期扭矩曲线**  
&emsp;&emsp;根据曲柄平衡移动距离推导出的调整后的预期扭矩曲线。

![预期扭矩曲线](../images/helpdoc/PNG/038.png?raw=true)

**（6） 运动特性曲线**  

![运动特性曲线](../images/helpdoc/PNG/039.png?raw=true)

#### 2.2.3.2 分析

&emsp;&emsp;显示计算分析结果参数及曲线，包括产量构成、泵效、系统效率、泵出入口参数等。

![分析](../images/helpdoc/PNG/007.png?raw=true)

#### 2.2.3.3 采集

&emsp;&emsp;显示传感器采集数据及曲线，包括通信状态、运行状态、油（套）压、电参数等。

![采集](../images/helpdoc/PNG/008.png?raw=true)

#### 2.2.3.4 控制

&emsp;&emsp;启停抽控制、频率控制以及数字化抽油机控制。数字化抽油机控制流程及操作项含义在附件1中有介绍。  
&emsp;&emsp;****操作方法：****  
&emsp;&emsp;如平衡调节上限，点击“设置”按钮，弹出选项框，选择“确定”按钮，输入设置的数值，输入密码，完成设置。

![控制](../images/helpdoc/PNG/009.png?raw=true)

<h2><a name="2.3全天评价"></a>2.3 全天评价</h2>

&emsp;&emsp;根据全天的采集数据与分析结果对单井进行全天评价。  
>- 运行时率、通信时率：累计值，当天的运行时率=运行时间/当天时间；  
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;以前的运行时率=运行时间/24小时；  
>- 移动距离、效率、液量、平衡度等：根据运行时率计算的加权平均值；  
>- 日用电量：累计值。

![统计](../images/helpdoc/PNG/010.png?raw=true)  

![目标井](../images/helpdoc/PNG/011.png?raw=true)

<h2><a name="2.4生产报表"></a>2.4 生产报表</h2>  

&emsp;&emsp;各参数计算方法与全天评价模块相同。

![生产报表](../images/helpdoc/PNG/013.png?raw=true)

<h2><a name="2.5图形查询"></a>2.5 图形查询</h2>

&emsp;&emsp;默认显示所有井最新地面功图，选择某一口井显示该井历史地面功图。

![图形查询](../images/helpdoc/PNG/014.png?raw=true)

<h2><a name="2.6权限管理"></a>2.6 权限管理</h2>

&emsp;&emsp;系统部署完成后需要新建单位、用户并划分权限。

<h3><a name="2.6.1单位管理"></a>2.6.1 单位管理</h3>

1、 使用系统管理员账号登录系统。  
2、 进入**单位管理**模块创建单位组织。如模拟油田公司—模拟采油厂—四矿。  
3、点击![创建按钮](../images/helpdoc/PNG/015.png?raw=true)，创建模拟油田公司；填写完成后，点击![保存按钮](../images/helpdoc/PNG/016.png?raw=true)，完成创建。  
>- 上级单位：由于模拟油田公司为根节点，上级单位不选择；  
>- 单位类别：按实际选择，局级；  
>- 单位名称：模拟油田公司；  
>- 单位编码、单位级别：确定上级单位、单位类别后自动生成；  
>- 单位说明：可不填写。 

![创建模拟油田公司](../images/helpdoc/PNG/040.png?raw=true)

4、 点击![创建按钮](../images/helpdoc/PNG/015.png?raw=true)，创建模拟采油厂；填写完成后，点击![保存按钮](../images/helpdoc/PNG/016.png?raw=true)，完成创建。  
>- 上级单位：已创建根节点，选择模拟油田公司；  
>- 单位类别：按实际选择，厂级；
>- 单位名称：模拟采油厂。  

![创建模拟采油厂](../images/helpdoc/PNG/041.png?raw=true)

5、 依次完成各级单位组织创建。

![创建模拟采油厂](../images/helpdoc/GIF/002.gif?raw=true)

<h3><a name="2.6.2用户管理"></a>2.6.2 用户管理</h3>

&emsp;&emsp;接下来进入**用户管理**模块，为不同的单位组织创建用户。点击![创建按钮](../images/helpdoc/PNG/015.png?raw=true)，创建新用户；填写完成后，点击![保存按钮](../images/helpdoc/PNG/016.png?raw=true)，完成创建。  
>- 单位名称：选择已创建的单位组织，确定组织的用户登录后，只能看到该组织及该组织的下属单位对应的信息；  
>- 角色：包括数字抽油机管理员、数字抽油机分析员；管理员可以对油井数据进行修改，对数字化抽油机进行控制；分析员只能查看相关诊断分析结果;  
>- 用户名称、用户账号、用户密码：按实际填写;
>- 用户电话、内部邮箱：可不填写;  
>- 快捷登录：在登录界面是否可以免密登录，一般用于数据查询人员。

![创建用户](../images/helpdoc/GIF/004.gif?raw=true)

<h2><a name="2.7数据配置"></a>2.7 数据配置</h2>

&emsp;&emsp;井名信息、生产数据、抽油机信息录入，可直接从编辑好的Excel中粘贴过来。

<h3><a name="2.7.1井名信息"></a>2.7.1 井名信息</h3>

#### 2.7.1.1 数据收集

>1. 单位名称：井所属单位，单位管理中创建的单位名称；
>2. 区块名称：井所属区块，**可不填写**；
>3. 井名；
>4. 举升类型：抽油机；
>5. 驱动名称：根据实际选择；
>6. 采集类型：根据该井的实际采集控制数据，选择驱动配置模块中创建的类型；
>7. 设备地址：RTU的SIM卡号码或MAC地址；
>8. 设备编号：1个RTU只连接1口井，则填写01；连接多口，则依次填写01、02、03...；
>9. 功图采集间隔：现场功图采集的时间间隔；
>10. 离散采集间隔：离散数据的采集间隔，如电流、电压等；
>11. 数据保存间隔：数据保存进数据库的时间间隔；
>12. 时率来源：DI信号（连接DI线）、电参计算（采集电参数据）、转速计算（螺杆泵井有转速数据可选择转速计算）、人工录入；
>13. 视频路径：监控视频的URL路径；
>14. 排序编号：井名在系统显示时的排序。

#### 2.7.1.2 数据录入

&emsp;&emsp;在Excel中编辑好后粘贴至井名信息模块中，可先点击导出按钮导出Excel模板。  
**注意：**  
**（1）录入时需要先在组织导航中选择录入井所在的组织，如四矿；否则会提示“请先选择组织节点”。**  
**（2）复制时序号列不要复制。**

![井名信息录入](../images/helpdoc/GIF/005.gif?raw=true)

#### 2.7.1.3 修改井名

&emsp;&emsp;在列表中修改井名，完成后点击![修改井名按钮](../images/helpdoc/PNG/012.png?raw=true)。  
**注意：**  
**（1）不要删除修改井，再重新录入新井，会导致历史数据丢失；**  
**（2）修改完成后，点击“修改井名”按钮，不要点击“保存”按钮。**

![修改井名](../images/helpdoc/GIF/006.gif?raw=true)

#### 2.7.1.4 删除数据

&emsp;&emsp;选中一行或多行，右键，选择删除行，然后点击![保存按钮](../images/helpdoc/PNG/033.png?raw=true)。

![删除数据](../images/helpdoc/GIF/007.gif?raw=true)

<h3><a name="2.7.2生产数据"></a>2.7.2 生产数据</h3>

#### 2.7.2.1 数据收集

>1. 生产时间：井名信息模块中**时率来源**为人工录入时填写，全天工作填写24，间抽按间抽时间填写，停井填写0；  
>2. 原油密度、水密度、天然气相对密度、饱和压力、油层中部深度、油层中部温度如果没有单井数据，可以参考所在区块数据；  
>3. 油压：未测油压数据可填写回压；  
>4. 泵级别：1、2、3；  
>5. 泵径：国标：28、32、38、44、51、57、63、70、83、95；API标准：26.99、31.8、38.1、44.5、45.2、50.8、57.2、63.5、69.9、82.6、95.3；  
>6. 套管内径：生产套管内径；  
>7. 抽油杆数据:  
>（1）抽油杆数据不包括光杆、泵上拉杆；  
>（2）对于某些井最后一级会有几十米的加重杆，例如外径28mm，长度50m，需收集；  
>（3）从井口到泵依次为一级杆、二级杆......，理论上除加重杆，外径逐级减小；  
>（4）杆的总长度应接近泵挂深度；  
>（5）杆级别：包括A、B、C、D、K、KD、HL、HY；  
>（6）杆内径：空心杆填写；
>8. 锚定状态：包括锚定和未锚定；抽油机井默认是未锚定；  
>9. 净毛比：用于产量标定，净毛比=实际产量/软件计算产量，默认为1，一般情况不修改。对于计产疑难井（油管漏、游动凡尔漏失、固定凡尔漏失），产量差距较大时，可以调整。例如：实际产量：20t/d，软件计算产量：40t/d，净毛比可设置在0.5左右。

#### 2.7.2.2 数据录入

&emsp;&emsp;收集完成后，复制粘贴到模块中。粘贴时无需按照模块列表中井顺序调整Excel表，直接粘贴保存即可。

![生产数据录入](../images/helpdoc/GIF/008.gif?raw=true)  

<h3><a name="2.7.3井身轨迹"></a>2.7.3 井身轨迹</h3>  

&emsp;&emsp;选择对应井名，将收集完成的井身轨迹数据（测量深度、井斜角、方位角）录入到“井身轨迹数据”中，点击“保存”按钮完成录入。  

![井身轨迹录入](../images/helpdoc/PNG/042.png?raw=true)

<h3><a name="2.7.4抽油机信息"></a>2.7.4 抽油机信息</h3>  

&emsp;&emsp;在计算**曲柄平衡移动距离**，给出优化建议时，需要用到部分抽油机数据，该部分数据可在对应厂家、型号的抽油机说明书中找到。  

#### 2.7.4.1 数据收集  

>1. 抽油机厂家、型号：查看对应抽油机的铭牌；
>2. 冲程：曲柄销孔对应的抽油机冲程，**可不填写**；
>3. 旋转方向：查看抽油机说明书；
>4. 曲柄偏置角：也称平衡相位角，一般对于异相型有偏置角，部分说明书中没有正负说明，应为负度数；
>5. 曲柄重心半径：查看抽油机说明书；
>6. 单块曲柄重量：包含曲柄销的重量，说明书中的曲柄重为两个曲柄的总重，单块曲柄重量为曲柄的总重/2+曲柄销重；
>7. 结构不平衡重：查看抽油机说明书；
>8. 平衡块位置：目前抽油机平衡块位置，需要现场确认，**可不填写**；
>9. 平衡块重量：确认抽油机平衡块数量，按抽油机说明书中对应的重量填写；
>10. 抽油机位置扭矩因数：**可不填写**。

**注意：**

>1. 平衡块位置和重量填写规则（例如4块平衡块）：  
平衡块位置（各位置之间“英文逗号”隔开）：0.5,1.2,0.5,1.5  
平衡块重量（各重量之间“英文逗号”隔开）：13.9,11.16,13.9,11.16  
>2. 如果抽油机说明书中数据单位与表格需求的不一致，要进行转换，比如1kg=0.0098kN。  

#### 2.7.4.2 数据录入

&emsp;&emsp;收集完成后，复制粘贴到模块中。  

![抽油机信息录入](../images/helpdoc/GIF/009.gif?raw=true)

<h3><a name="2.7.5驱动配置"></a>2.7.5 驱动配置</h3>

&emsp;&emsp;针对不同的设备安装情况设置不同的采集项和控制项。

**1、采集项**
>- 运行状态；
>- 生产数据：包括油压、套压、回压、井口油温、动液面、含水率；
>- 电参数据：A/B/C相电流、A/B/C相电压、有功功耗、无功功耗、有功功率、无功功率、反向功率、功率因数；
>- 变频数据：变频运行频率；
>- 功图数据：采集时间、功图点数、冲次、冲程、曲线位移值、曲线载荷值、曲线电流值、曲线功率值、功图采集间隔、功图采集设置点数；
>- 螺杆泵特有数据：转速、转矩；
>- 平衡调节：远程调节状态。

**2、控制项**  
>- 即时调节；
>- 启停抽；
>- 远程调节手自动模式；
>- 变频设置频率；
>- 功图数据采集间隔；
>- 离散数据采集间隔；
>- 电流上/下限；
>- 功率上/下限；
>- 向远离/接近驴头方向调节距离；
>- 平衡计算方式；
>- 参与平衡计算冲程次数；
>- 平衡调节上/下限；
>- 重心远离/接近支点每拍调节时间

&emsp;&emsp;点击![创建按钮](../images/helpdoc/PNG/015.png?raw=true)创建采控类型，如类型名称“类型八”，类型编码“type8”，类型描述“数字化抽油机数据”，创建完成后，在右侧列表中勾选实际采集项和控制项，点击![保存按钮](../images/helpdoc/PNG/033.png?raw=true)完成配置。后续在**井名信息**模块数据录入时按照单井实际采控项选择不同的采集类型。

![驱动配置](../images/helpdoc/PNG/017.png?raw=true)

<h3><a name="2.7.6计算维护"></a>2.7.6 计算维护</h3>

&emsp;&emsp;计算维护模块主要应用场景包括：  
>- 针对系统部署初期或现场设备安装初期，各井的生产数据并未收集或收集的不完整，在进行功图诊断及产量计算时采用了模拟数据，待后续生产数据收集完整后，需要对历史数据进行重新计算。  
>- 生产数据收集的部分数据有误，更正后需要重新计算。  
>- 在使用过程中，现场作业后并未及时更新生产数据。  
>- 其他需要对历史数据进行重新计算的情况。

**注意：**  
>- 在“生产数据”模块中修改参数只对后续的计算起作用，对已经计算完成的历史数据并不生效。如果想要对历史结果重新计算，需要在“计算维护”模块中进行。  
>- 历史结果会被重新计算的结果覆盖。  
>- 0或2为未计算，1为计算完成，-99为计算错误，请检查生产数据。

&emsp;&emsp;对历史结果进行重新计算有两种方法，根据实际情况选择较为便捷的方法：  
**1、修改数据计算**  
&emsp;&emsp;选择目标井，找到需要修改的某条记录或某个时间段的多条记录，修改完生产数据后，点击“修改数据计算”按钮进行重新计算。  
&emsp;&emsp;例如：修改S68112井，2019年2月24号全部功图采集时间的泵径数据并重新计算。  
&emsp;&emsp;操作：井名中选择S68112，时间范围选择2019-02-24至2019-02-24，列表中将泵径38mm修改为44mm，点击“修改数据计算”按钮。

![修改数据计算](../images/helpdoc/PNG/018.png?raw=true)

**2、关联数据计算**  
&emsp;&emsp;利用生产数据表中的最新生产数据对某口井或所有井某个时间段内的所有历史结果进行重新计算。  
（1）单井关联数据计算  
&emsp;&emsp;例如：修改S68112井，2019年1月24日至2019年2月24日内的所有历史结果。  
&emsp;&emsp;操作：“生产数据”模块中已录入最新生产数据，“计算维护”模块中井名选择S68112，时间范围2019-01-24至2019-02-24，点击“关联数据计算”。弹出操作确认对话框，确认无误后点击“是”。这时，S68112井2019年1月24日至2019年2月24日的所有历史数据将按最新的生产数据进行重新计算。

![单井关联数据计算](../images/helpdoc/PNG/019.png?raw=true)

（2）所有井关联数据计算  
&emsp;&emsp;例如：单位组织下所有井，2019年1月24日至2019年2月24日内的所有历史结果。  
&emsp;&emsp;操作：“生产数据”模块中已录入最新生产数据，“计算维护”模块中井名不选择或选择全部，时间范围2019-01-24至2019-02-24，点击“关联数据计算”。弹出操作确认对话框，确认无误后点击“是”。这时，所有井2019年1月24日至2019年2月24日的所有历史数据将按最新的生产数据进行重新计算。

![所有井关联数据计算](../images/helpdoc/PNG/020.png?raw=true)

<h2><a name="2.8系统配置"></a>2.8 系统配置</h2>

<h3><a name="2.8.1字典配置"></a>2.8.1 字典配置</h3>

&emsp;&emsp;对各模块显示的字段进行管理，主要修改字段名称、显示顺序、是否显示等。如“抽油机实时评价_功图工况”（即实时评价模块中功图工况子标签中的列表项）中是否显示在线时率或运行时率相关参数，可点击对应字典项，并在里面进行勾选。

![字典配置](../images/helpdoc/PNG/022.png?raw=true)

<h3><a name="2.8.2统计配置"></a>2.8.2 统计配置</h3>

&emsp;&emsp;配置各项参数的统计级别。如设置功率平衡度的界限范围值，可点击对应相，并在里面进行修改。

![统计配置](../images/helpdoc/PNG/023.png?raw=true)

<h3><a name="2.8.3报警配置"></a>2.8.3 报警配置</h3>

&emsp;&emsp;设置报警级别、开关、颜色等。

![报警配置](../images/helpdoc/PNG/024.png?raw=true)  

<h1><a name="附件1数字化抽油机"></a>附件1 数字化抽油机</h1>  

<h2><a name="F1.1智能机柜操作说明"></a>F1.1 智能机柜操作说明</h2>  

![智能机柜](../images/helpdoc/PNG/050.png?raw=true)

>1. 电源开关：拨动开关到下位置，即可关闭整个智能机柜，拨动开关到上位置，智能机柜通电。
>2. 电源指示灯：接通电源后亮起。
>3. 前进灯：在手动调节模式下，“手动调节”旋钮打至“前”时亮起，平衡电机向前移动。
>4. 后退灯：在手动调节模式下，“手动调节”旋钮打至“后”时亮起，平衡电机向后移动。
>5. “平衡调节”旋钮：旋转至“手动”位置，操作人员可在现场操作“手动调节”旋钮，此时上位机软件远程调节和RTU自动调节失效；旋转至“自动”位置，上位机软件和RTU自动调节可执行，现场手动调节失效；旋转至“锁定”位置，现场手动调节和远程自动调节均失效。
>6. “手动调节”旋钮：只有在“平衡调节”旋钮打至“手动”位置才生效。在生效状态下，“手动调节”打至“前”，尾部平衡块将向接近驴头位置移动，直至尾部平衡块抵达“前限位”平衡电机停止工作。“手动调节”打至中间位置不工作；在将“手动调节”打至“后”，尾部平衡块将向远离驴头位置移动，直至尾部平衡块抵达“后限位”平衡电机停止工作。或“手动调节”打至中间位置，如此往复调节平衡电机的“前” “后”。
>7. 智能机柜内工作电压AC220V，抽油机尾部平衡前后限位开关电压为安全电压DC12V。
>8. 智能机柜具有缺相、短路、过载、过热、过流保护功能。

<h2><a name="F1.2自动调节控制流程"></a>F1.2 自动调节控制流程</h2>  

>1. 正常油井生产数据采集工作中不进行平衡调节，仅仅对平衡度进行监测，给出曲柄平衡移动距离；  
>2. 控制器接收到“远程调节手自动模式”为“自动”时，触发平衡度自动调节工作；  
>3. 以“平衡调节上限”、“平衡调节下限”区间为目标进行调节；每次调节通过设定好的“重心远离支点每拍调节时间”、“重心接近支点每拍调节时间”来控制平衡块的位移量；每次调节完成后，根据“参与平衡度计算的冲程次数”重新计算平衡度，重复以上过程直至达标；  
>4. 在平衡调节过程中，检测到DI状态的平衡块限位状态为限位时，立即中止相应调节过程。 

<h2><a name="F1.3平衡度判断方法"></a>F1.3 平衡度判断方法</h2>  

&emsp;&emsp;根据设置的冲程次数，如3次（默认1次），计算连续3次冲程，根据3次冲程的下冲程电流最大值与上冲程电流最大值之比的平均值计算平衡度，如果平衡度不在设定的范围内（默认为85%-115%），自动移动尾部平衡装置，如果平衡度在设定的范围内（默认为85%-115%），尾部平衡装置不移动。接下的3次冲程，继续以此判断，直至达标。如果调整达到限位点，则显示到达限位点。此时必须现场调整曲柄平衡块，无法自动调整。  

<h2><a name="F1.4操作项含义"></a>F1.4 操作项含义</h2>  

&emsp;&emsp;“实时评价”模块 — “控制”中各操作项含义：  
>1. 即时采集：立即采集一组离散数据并待RTU功图采集完成后进行功图采集；；
>2. 运行状态：控制抽油机启停抽；
>3. 远程调节手自动模式：抽油机尾部的平衡电机根据平衡度自动调节或人工下发调节距离
>4. 变频设置频率(Hz)；
>5. 功图数据采集间隔(min)；
>6. 离散数据采集间隔(min)；
>7. 电流上/下限(A)：设置电流报警上限/下限；
>8. 功率上/下限(kW)：设置功率报警上限/下限；
>9. 向远离驴头方向调节距离(cm)：发送调节距离控制尾平衡块向远离驴头方向移动，单次调节范围0~20cm；
>10. 向接近驴头方向调节距离(cm)：发送调节距离控制尾平衡块向接近驴头方向移动，单次调节范围0~20cm；
>11. 参与平衡计算冲程次数：根据设置的“参与平衡计算冲程次数”，如3次，计算连续3次冲程，根据3次冲程的下冲程电流或有功功率最大值与上冲程电流或有功功率最大值之比的平均值计算平衡度，自动移动尾部平衡装置。接下的3次冲程，继续以此判断，直至平衡度达标。**默认为1次，一般不用修改**。
>12. 平衡调节上/下限(%)：默认平衡度上限为100%，下限为85%；
>13. 平衡度判断方式：电流法或功率法；
>14. 平衡远程自动调节：允许或不允许自动调平衡;
>15. 平衡前限位：判断尾部平衡块是否可以向接近驴头方向移动，未限位时可以移动，限位时不可移动；如果调整达到限位点，则显示“限位”。此时必须现场调整平衡块，无法自动调整；
>16. 平衡后限位：判断尾部平衡块是否可以向远离驴头方向移动，未限位时可以移动，限位时不可移动。如果调整达到限位点，则显示“限位”。此时必须现场调整曲柄平衡块，无法自动调整。
  
<h2><a name="F1.5曲柄平衡移动距离"></a>F1.5 曲柄平衡移动距离</h2>  

&emsp;&emsp;软件根据采集的电功图（有功功率图），结合平衡块重量等抽油机参数，给出曲柄平衡块向内或向外移动距离建议，当尾平衡块限位时，可根据该建议调整曲柄平衡块，使抽油机达到平衡状态。  
&emsp;&emsp;所需抽油机参数在2.7.4节有详细说明。  
&emsp;&emsp;功率平衡度=下冲程有功功率最大值/上冲程有功功率最大值

<h2><a name="F1.6电参工况"></a>F1.6 电参工况</h2>  

&emsp;&emsp;电参工况由前端RTU判断完成后，上传至平台。如有多种工况同时报警，以组合形式上传，如电流超上限报警/功率超上限报警。

| **序号** | **代码** | **名称**             |
|----------|----------|----------------------|
|1         | 0        | 正常                 |
|2         | 1        | 电压缺相             |
|3         | 2        | 电流超上限报警       |
|4         | 4        | 电流超下限报警       |
|5         | 8        | 功率超上限报警       |
|6         | 16       | 功率超下限报警       |
|7         | 32       | 电参模块故障         |