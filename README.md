# swaiot_tools
Swaiot 物端设备对接工具（SDK动态生成工具）
# SWAIOT物端对接工具使用指南

### 简介：

​	swaiot iot-tools是一个用于快速对接创维物联网平台的物端SDK生成工具。通过可视化的配置：平台、属性、功能等参数，自动生成对接SDK的接口与回调函数。在尽可能减少代码出错问题的同事，实现快速对接“创维IOT”平台的能力。您可以按照如下地址得到安装包文件：

​	工具及说明下载地址：

​	https://github.com/swaiot/swaiot_tools

​	*本说明版权属于 深圳创维-RGB电子有限公司，由SWAIOT实验室维护。如有更改，恕不另行通知。20206.16*

------



### 使用说明：

​	下面您可以根据如下说明，生成设备端对接SDK用于快速接入创维物联网系统。

###### 工具简介

​	首先请根据平台下载iot-tools的安装包，并安装应用。在安装完成后会直接打开工具，同时在桌面生成应用图标。工具基本界面如下图：

![](https://docman.skyworthiot.com/uploads/prod-access-doc/images/m_372b992b6ce1222172d7dc308b9cdb17_r.png)

​	工具首页中简单描述了工具的使用方式。您可以在左侧功能栏中切换配置页，并最终导出自动配置好的SDK对接代码。

​	同时工具中还提供了一个微型的“指令调试助手”，用于协助您在没有物联网模块的情况下进行MCU调代码调试。

------



###### 平台设置

​	平台设置的主要功能是用于区分不同MCU带来的：大小端问题、整型（int）的位数问题、以及C51平台的内存寻址区域问题等。您可以根据您所使用的MCU平台来配置相关设置。默认 Arm Cortex-M系类使用小端+int32，C51及其兼容芯片使用大端+int16的形式。下图为平台设置界面。您可以点击选项卡进行详细配置。（默认支持Cortex-M内核MCU）

![](https://docman.skyworthiot.com/uploads/prod-access-doc/images/m_fb61469130abcbe0a042f2dd82de3f34_r.png)

​	**“平台选择”**：点击平台设置选项卡后界面：

![](https://docman.skyworthiot.com/uploads/prod-access-doc/images/m_c1657ccf72763d6142a4db098b03c253_r.png)

​	**“缓存区寻址区域”**：C51需要注意缓存区的寻址区域的选择，每次操作后，软件会记住上一次的设置，如需更改请注意。

------

![](https://docman.skyworthiot.com/uploads/prod-access-doc/images/m_61dc032b691770d5607f8d248ef36b2a_r.jpg)

###### 功能设置

​	功能设置的主要目的是优化SDK所需要的功能。比如说通讯协议中只使用了int8（Byte）变量，那么所有为int16、int32、float等服务的代码便都是冗余的。“功能设置”可以可视化的帮您进行代码裁切。

![](https://docman.skyworthiot.com/uploads/prod-access-doc/images/m_66c1ef745ceb7a3b8888935d4e2b9180_r.png)

​	**“支持智慧屏功能”**：将对SDK添加心跳自动回复功能，以及sn码设置相关回调函数。



![](https://docman.skyworthiot.com/uploads/prod-access-doc/images/m_ce68c62a7c6bcb81f284c0e8642210a9_r.png)

​	**“支持属性类型”**：将改变默认支持的属性类型，与属性设置联动。（如果如果关闭了部分类型，即使属性设置中纯在遗留的属性项，最终页不会导出与此类型相关的接口）

![](https://docman.skyworthiot.com/uploads/prod-access-doc/images/m_8619d66a2817f85009f056652548b1d2_r.png)

​	**“可选扩展功能”**：（WIFI物联模块的专属功能，智慧屏不支持），请根据需求选择添加功能

![](https://docman.skyworthiot.com/uploads/prod-access-doc/images/m_b71b875315138400a3bd0cddc5b91c58_r.png)

------

###### 属性设置

​	属性设置的主要功能是设置产品“三元组”（产品类型、产品型号、厂家代号）、设置产品通讯属性。具体属性与三元组可通过siaiot开放平台获取，或从对接工程师处索取。*（需要注意的是添加通讯属性中的数据类型是通过“功能设置而联动的”，如果在已经添加了部分属性后修改了“支持属性”，那么最终代码中将不会体现这些已取消类型的属性。纵然这些属性已经被写进属性列表，但代码中不会体现。）*

![](https://docman.skyworthiot.com/uploads/prod-access-doc/images/m_f4b3049296ce1b023e50a9ac725e86b5_r.png)

​	**“设置三元组”**：设置产品类型id、产品型号（字符串）、厂家ID。类型编号指的是产品所属的类型，比如洗衣机，台灯等等，这个可以产品类型表,品牌编号指的是品牌代码，比如创维:1，产品型号指的是产品自己的型号，比如净水器：T5A，产品型号名字符长度不能超过8个字符，不能有分号。

![](https://docman.skyworthiot.com/uploads/prod-access-doc/images/m_6e705a7de289c9ed38e0e077a83b9bec_r.png)

​	**“添加通讯属性”**：属性指的是需要与APP端进行交互的信息，属性名称需要选择选择数据类型。属性的个数最多有31个。属性名称最多8个字符，为了更方便的与合作方沟通，建议填写属性备注，有利于双方工作更好的展开。

 可以重新编辑和删除属性。

![](https://docman.skyworthiot.com/uploads/prod-access-doc/images/m_ff6de695a5bc0c2a17ca96f47952d30b_r.png)

###### 优化设置

​	默认无需修改优化设置。在MCU的RAM或ROM不足时，可以通过修改或者关闭循环缓冲区，用于减少系统消耗。

![](https://docman.skyworthiot.com/uploads/prod-access-doc/images/m_76cf295133bbef2e7df376a09ed949c7_r.png)

*（注意，应答设置本身不会明显减少系统消耗，因此建议保持周期答复模式）*

​	**“缓冲设置”**：打开循环缓冲区后，缓冲区的大小可以进行设置，byte旁边的数字表示最大支持4位数。

![](https://docman.skyworthiot.com/uploads/prod-access-doc/images/m_a0a20fa4bd81df1090282627fdbb0abc_r.jpg)

​	**“答复设置”**：有两种答复，直接答复和延迟答复。直接答复一调用发送函数就会被触发需要手动设置200ms后的答复，延迟答复是已经设置好200m后在发送（建议使用周期答复）

![](https://docman.skyworthiot.com/uploads/prod-access-doc/images/m_aef4f6a2c13c5765fdd592aac0bdcfd4_r.png)

------

###### 导出设置

​	选择好输出路径之后，点击导出配置代码

![](https://docman.skyworthiot.com/uploads/prod-access-doc/images/m_a8c15ce6c6d746d5321053511b67b9cc_r.png)

​	**“生成的文件”**：生成的文件夹名就是swaiot,里面包含代码文件和属性表，请将swaiot文件添加到产品工程中，编译需要将swaiot和swaiot/lib添加到include路径中。

​	其中

​	product_config.xlsx文件：设置信息一览表，您可以将表格中的预留信息填写清楚，用于内部对接以及资料归档。

​	iot_receive_handler.c文件：自动生成的回调函数，用于处理模块或者智慧屏下发的指令。

​	iot_user_config.h文件：自动生成的函数函数接口，内部包含了所有可用的函数接口。

​	lib文件夹：物联网协议依赖文件夹。无需阅读。

![](https://docman.skyworthiot.com/uploads/prod-access-doc/images/m_4e5c1143280729fa2c7ab7f7dd880f77_r.png)



###### 调试工具

​	为了应对部分开发过程中缺少开发模块或app调试界面，又或者无法快速解析模块传输数据的问题，我们提供了一个简单的调试工具用模拟模块功能以及解析发送数据。

![](https://docman.skyworthiot.com/uploads/prod-access-doc/images/m_fd5b6528611e27e18493221867d5e7c5_r.png)

​	用电脑通过串口与MCU相连，使用调试工具模拟wifi模块或者智慧屏幕的相关指令是否正确。

​	点击“发送通讯属性”后，可以看到一份和“属性设置”中属性相同的属性表，用于模拟云端与物端的数据通讯、解码、格式是否正常。

![](https://docman.skyworthiot.com/uploads/prod-access-doc/images/m_520f6575b2ae821a90e646a19575459f_r.png)
