---
title: 如何定义自定义数据类型
description: 如何定义自定义数据类型
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bc18de02594114d5fcc31abac050a28b4cd13157
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96795617"
---
# <a name="how-do-you-define-custom-data-types"></a>如何定义自定义数据类型？


Windows (ETW) 的事件跟踪定义了用于跟踪函数的几个简单和复杂类型。 这些类型在 Defaultwpp.ini 文件中声明。 不过，您可以创建自己的自定义数据类型。

如果要声明变量并使用有意义的字词（而不是整数）来描述变量的值，则可以使用自定义数据类型。

例如， *DiskState* 变量包含磁盘的状态。 下面是 *DiskState* 的值：

```
DiskOffline = 0
DiskOnline = 1
DiskFailed = 2
DiskStalled = 3
```

您可以定义一个名为 *DiskState* 的自定义类型，以获取显示 "DiskState 失败" 的跟踪消息，而不是在跟踪消息中读取 "DiskState = 2"，然后再查找含义 **2**。

### <a name="span-idcreating_a_custom_data_typespanspan-idcreating_a_custom_data_typespancreating-a-custom-data-type"></a><span id="creating_a_custom_data_type"></span><span id="CREATING_A_CUSTOM_DATA_TYPE"></span>创建自定义数据类型

若要创建自定义数据类型，请完成以下步骤：

1.  创建具有 .ini 文件扩展名的本地配置文件，如 localwpp.ini。 不能将自定义类型添加到头文件或源文件中。

2.  使用 TYPEMACRO 常量定义自定义数据类型。

3.  标识源或标头文件中的配置数据。

4.  将 **-ini** 参数添加到 \_ 源文件中的 RUN WPP 宏。

5.  在跟踪消息中使用自定义数据类型。

### <a name="span-iddefining_a_typemacro_constantspanspan-iddefining_a_typemacro_constantspandefining-a-typemacro-constant"></a><span id="defining_a_typemacro_constant"></span><span id="DEFINING_A_TYPEMACRO_CONSTANT"></span>定义 TYPEMACRO 常量

定义具有以下格式的 TYPEMACRO 常量。 这些值定义为字符串列表。

```
TYPEMACRO(Type,{ItemListLong | ItemListShort | ItemListByteShort | ItemListByteLong},(Value1,Value2...));
```

其中：

<span id="ItemListShort"></span><span id="itemlistshort"></span><span id="ITEMLISTSHORT"></span>**ItemListShort**  
16位带符号整数。

<span id="ItemListLong"></span><span id="itemlistlong"></span><span id="ITEMLISTLONG"></span>**ItemListLong**  
带符号或无符号32位整数。

<span id="ItemSetByteShort"></span><span id="itemsetbyteshort"></span><span id="ITEMSETBYTESHORT"></span>**ItemSetByteShort**  
16位带符号位值。

<span id="ItemSetByteLong"></span><span id="itemsetbytelong"></span><span id="ITEMSETBYTELONG"></span>**ItemSetByteLong**  
带符号或无符号32位值。

例如：

```
TYPEMACRO(DiskState,ItemListLong(DiskOffline,DiskOnline,DiskFailed,DiskStalled));
```

### <a name="span-ididentifying_the_configuration_dataspanspan-ididentifying_the_configuration_dataspanidentifying-the-configuration-data"></a><span id="identifying_the_configuration_data"></span><span id="IDENTIFYING_THE_CONFIGURATION_DATA"></span>标识配置数据

如果将自定义数据类型添加到包含其他代码的文件（如源文件或头文件），请使用 **begin \_ wpp config** 和 **end \_ wpp** 语句来标识文件中的配置数据。 例如：

```
// begin_wpp config
    //TYPEMACRO(DiskState,ItemListLong(DiskOffline,DiskOnline,DiskFailed,DiskStalled));
// end_wpp
```

如果将自定义数据类型添加到本地配置文件，则不需要 **begin \_ wpp config** 和 **end \_ wpp** 语句。

### <a name="span-idadd_the__ini_parameterspanspan-idadd_the__ini_parameterspanadd-the--ini-parameter"></a><span id="add_the__ini_parameter"></span><span id="ADD_THE__INI_PARAMETER"></span>添加-ini 参数

为自定义类型创建本地配置文件时，需要将 **-ini** 参数添加到 \_ 调用 wpp 预处理器的 RUN WPP 语句中。

**-Ini** 参数指示 ETW 在配置文件中搜索配置数据 ( .ini) ，以及使用 Defaultwpp.ini。 例如：

```
RUN_WPP -km -ini:localwpp.ini
```

> [!IMPORTANT]
> 不能在用户模式应用程序或动态链接库的 "运行 WPP" 指令中指定 **-公里** 开关 \_ (dll) 。

 

### <a name="span-idusing_the_custom_data_typespanspan-idusing_the_custom_data_typespanusing-the-custom-data-type"></a><span id="using_the_custom_data_type"></span><span id="USING_THE_CUSTOM_DATA_TYPE"></span>使用自定义数据类型

定义自定义数据类型后，可以在跟踪消息中使用它。 在该类型名称之前加上百分号 (**%**) 并将其用惊叹号括起来 (！ ) 。 例如：

```
DoTraceMessage(INFO,"Disk State is %!diskstate!",DiskState); 
```

生成的跟踪消息使用您定义的常数来表示值：

```
DiskState is Offline.
```
