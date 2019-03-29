---
title: 如何定义自定义数据类型
description: 如何定义自定义数据类型
ms.assetid: 849f83ae-5fe7-447b-9d02-3d980757bf7d
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3bb1889b4508fff579fbe6ca241c53363d0bde74
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567335"
---
# <a name="how-do-you-define-custom-data-types"></a>如何定义自定义数据类型？


Windows 事件跟踪 (ETW) 跟踪函数中定义使用的几个简单和复杂类型。 Defaultwpp.ini 文件中声明这些类型。 但是，可以创建自己的自定义数据类型。

当你想要声明变量和使用有意义的术语-而不是整数-来描述这些变量的值时使用自定义数据类型。

例如， *DiskState*变量包含磁盘的状态。 以下是值的*DiskState*:

```
DiskOffline = 0
DiskOnline = 1
DiskFailed = 2
DiskStalled = 3
```

而不是读取"DiskState = 2"中跟踪消息，然后无需查找的含义**2**，可以定义一个名为的自定义类型*DiskState*，以获取跟踪消息，指出"DiskState 失败。"

### <a name="span-idcreatingacustomdatatypespanspan-idcreatingacustomdatatypespancreating-a-custom-data-type"></a><span id="creating_a_custom_data_type"></span><span id="CREATING_A_CUSTOM_DATA_TYPE"></span>创建自定义数据类型

若要创建自定义数据类型，请完成以下步骤：

1.  创建具有.ini 文件扩展名，如 localwpp.ini 的本地配置文件。 不能将自定义类型添加到标头或源文件。

2.  使用 TYPEMACRO 常量来定义自定义数据类型。

3.  标识源或标头文件中的配置数据。

4.  添加 **-ini**参数运行\_WPP 宏在源文件中的。

5.  在跟踪消息中使用自定义数据类型。

### <a name="span-iddefiningatypemacroconstantspanspan-iddefiningatypemacroconstantspandefining-a-typemacro-constant"></a><span id="defining_a_typemacro_constant"></span><span id="DEFINING_A_TYPEMACRO_CONSTANT"></span>定义一个 TYPEMACRO 常量

定义一个 TYPEMACRO 常量，它采用以下格式。 值被定义为字符串的列表。

```
TYPEMACRO(Type,{ItemListLong | ItemListShort | ItemListByteShort | ItemListByteLong},(Value1,Value2...));
```

其中：

<span id="ItemListShort"></span><span id="itemlistshort"></span><span id="ITEMLISTSHORT"></span>**ItemListShort**  
16 位带符号的整数。

<span id="ItemListLong"></span><span id="itemlistlong"></span><span id="ITEMLISTLONG"></span>**ItemListLong**  
有符号或无符号 32 位整数。

<span id="ItemSetByteShort"></span><span id="itemsetbyteshort"></span><span id="ITEMSETBYTESHORT"></span>**ItemSetByteShort**  
带符号的 16 位的位值。

<span id="ItemSetByteLong"></span><span id="itemsetbytelong"></span><span id="ITEMSETBYTELONG"></span>**ItemSetByteLong**  
有符号或无符号 32 位值。

例如：

```
TYPEMACRO(DiskState,ItemListLong(DiskOffline,DiskOnline,DiskFailed,DiskStalled));
```

### <a name="span-ididentifyingtheconfigurationdataspanspan-ididentifyingtheconfigurationdataspanidentifying-the-configuration-data"></a><span id="identifying_the_configuration_data"></span><span id="IDENTIFYING_THE_CONFIGURATION_DATA"></span>标识的配置数据

如果自定义数据类型添加到具有其他代码，如源文件或头文件的文件，则使用**开始\_wpp config**并**最终\_wpp**语句以标识配置文件中的数据。 例如：

```
// begin_wpp config
    //TYPEMACRO(DiskState,ItemListLong(DiskOffline,DiskOnline,DiskFailed,DiskStalled));
// end_wpp
```

如果自定义数据类型添加到本地配置文件，则**开始\_wpp config**并**最终\_wpp**语句，则不需要。

### <a name="span-idaddtheiniparameterspanspan-idaddtheiniparameterspanadd-the--ini-parameter"></a><span id="add_the__ini_parameter"></span><span id="ADD_THE__INI_PARAMETER"></span>添加-ini 参数

创建自定义类型的本地配置文件时，需要将添加 **-ini**参数运行\_WPP WPP 预处理器将调用的语句。

**-Ini**参数指示除了使用 Defaultwpp.ini ETW 搜索配置文件 (.ini) 中的配置数据。 例如：

```
RUN_WPP -km -ini:localwpp.ini
```

> [!IMPORTANT]
> 您必须指定**公里**在运行中切换\_WPP 指令用于用户模式应用程序或动态链接库 (Dll)。

 

### <a name="span-idusingthecustomdatatypespanspan-idusingthecustomdatatypespanusing-the-custom-data-type"></a><span id="using_the_custom_data_type"></span><span id="USING_THE_CUSTOM_DATA_TYPE"></span>使用自定义数据类型

定义自定义数据类型后，可以使用它跟踪消息中。 类型名称前面加上百分号 (**%**)，请在它两边使用感叹号 （！）。 例如：

```
DoTraceMessage(INFO,"Disk State is %!diskstate!",DiskState); 
```

生成的跟踪消息使用定义来表示值的常量：

```
DiskState is Offline.
```
