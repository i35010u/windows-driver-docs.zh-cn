---
title: 简单数据评估语言概述
description: WDTF 提供用于简化收集基于属性或关系的目标的任务的简单查询语言。
ms.assetid: 84c2a1d6-6bec-4aeb-b858-c29f50d74390
keywords:
- 测试框架 WDK，SDEL 的 Windows 设备
- WDTF WDK SDEL
- 简单数据评估语言 WDK WDTF
- SDEL WDK WDTF
- 查询语言 WDK WDTF
- 目标对象 WDK WDTF
- 命名空间 WDK WDTF
- 关系基于测试 WDK WDTF
- 关系说明符 WDK WDTF
- 命名的查询 WDK WDTF
- WDK WDTF 属性
- 布尔逻辑 WDK WDTF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1505fcacd17be2590a8a85bc3bbdfd06e82c0472
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63355454"
---
# <a name="simple-data-evaluation-language-overview"></a>简单数据评估语言概述


WDTF 提供用于简化收集基于属性或关系的目标的任务的简单查询语言。 简单数据评估语言 (SDEL) 是类似于 XPath。 有关 XPath 的详细信息，请参阅[XPath 参考](https://go.microsoft.com/fwlink/p/?linkid=33165)。

在本主题中的以下部分介绍如何使用 SDEL。

**请注意**  命名空间的所有令牌内它们的属性标记的完整列表，请参阅[SDEL 令牌](https://msdn.microsoft.com/library/windows/hardware/ff539571)。

 

### <a name="sdel-syntax-basics"></a>SDEL 语法基础知识

SDEL 使用属性的令牌来执行匹配项并检索数据。 所有 SDEL 令牌只能都包含字母数字字符和连字符 （-）。

*特性*指一段附加到的目标数据。 属性中的实际值存储为**变体**。 如果将后跟一个比较运算符*测试*后 SDEL 属性值将执行比较的匹配。 应将测试值放置在单或双引号括起来-此表示法，您可以使用你测试的值，但不同时实际单或双引号括起来。 如果测试值包含仅字母数字字符和连字符 （-），则可以省略引号引起来。

### <a name="comparison-operations"></a>比较操作

SDEL 允许各种比较运算符以按照特性标记。 在比较时，到运算符左侧的属性中的实际值进行，以便为通过运算符右侧的测试值相同的类型**VariantChangeType**方法 （这在 Microsoft 中所述Windows SDK 文档）。 下表显示不同的比较运算符 SDEL 支持。

比较运算符的含义相等 （=）

类型可进行更改后，它们通过使用比较**VarCmp**方法 （这 Windows SDK 文档中所述）。

不等于 (！ =)

小于 (&lt;)

小于或等于 (&lt;=)

大于 (&gt;)

大于或等于 (&gt;=)

位与 (&)

此运算符将强制类型转换成 VT\_I8 之前执行的实际的按位 AND 和测试值。

指定不比较运算 （和任何值）

如果该属性中的实际值是类型 VT\_BOOL，匹配是满足根据此值-即，不需要执行的比较运算符"IsDisableable = True"。 否则为如果根本没有任何值 (VT 以外\_空)，匹配不满意。

 

如果有多个实际值 （或数组） 的属性中，所有比较运算符应解释以匹配至少一个，除非不相等运算符，它具有相反的行为。 如果不能在所有比较类型 (即**VariantChangeType**失败)，没有匹配项 （与不相等运算符，它具有相反的行为除外）。

### <a name="understanding-attribute-namespaces"></a>了解属性命名空间

SDEL 使用的属性进行分组的命名空间标记。 命名空间的所有令牌内它们的属性标记的完整列表，请参阅[SDEL 令牌](https://msdn.microsoft.com/library/windows/hardware/ff539571)。

若要使用的根命名空间之外的任何属性，您必须具有命名空间名称，然后两个冒号 （:） 的属性的前缀。 下面的 VBScript 代码示例显示 Disk::IsRemovable 属性的值。

```cpp
WScript.Echo "Is Removable?: " & DeviceObj.GetValue("Disk::IsRemovable")
```

### <a name="examining-a-target-by-using-getvalue-and-eval"></a>检查目标使用 GetValue 和评估版

[ **IWDTFTarget2::GetValue** ](https://msdn.microsoft.com/library/windows/hardware/hh439403)方法允许你询问有关其属性的目标。 下面的 VBScript 代码示例将的值打印[FriendlyName](https://msdn.microsoft.com/library/windows/hardware/ff539571)目标属性。

```cpp
WScript.Echo "FriendlyName: " & Device.GetValue("FriendlyName")
```

特性标记的完整列表，请参阅[SDEL 令牌](https://msdn.microsoft.com/library/windows/hardware/ff539571)。

此外可以使用[ **IWDTFTarget2::Eval** ](https://msdn.microsoft.com/library/windows/hardware/hh439396)方法计算的 SDEL 语句针对的目标。 **Eval**将返回**变体\_TRUE**或**变体\_FALSE**。 下面的 VBScript 代码示例使用**Eval**以确定是否可以禁用设备。

```cpp
If Device.Eval("IsDisableable=true") Then 
    WScript.Echo "Target is disableable!"
End If
```

此外可以使用[ **Eval** ](https://msdn.microsoft.com/library/windows/hardware/hh439396)测试属性是否存在。 当传递**Eval**属性，但没有比较运算符或值， **Eval**将返回**变体\_TRUE**属性或命名空间包含的任何值 （如果以外**VT\_空**)。 下面的 VBScript 代码示例使用**Eval**来确定目标是否具有 SymbolicLink 关键字。

```cpp
If Device.Eval("SymbolicLink") Then 
    WScript.Echo "Target has a SymbolicLink!"
End If
```

此外，缺少比较运算符，但包含的特性**VT\_BOOL**具有应用于它们的隐式 = true 比较值。 此隐式比较，则意味着"IsDisableable"等效于"IsDisableable = 'true'"。

### <a name="navigating-relationships"></a>导航关系

测试经常涉及检查相关的设备更改状态时，会发生什么情况。 例如，禁用的 USB 集线器后，不要附加到其中的设备状态更改正确处理？ 此外，你可能想要定位根据相关的设备中信息的设备。 若要支持此功能，SDEL 包括之前的任何属性或命名空间 （但不是晚于其中任一） 指定一个或多个逻辑关系的方法。 关系令牌由正斜杠 （/） 分隔的属性或命名空间中。 下面的 VBScript 代码示例将的值打印[FriendlyName](https://msdn.microsoft.com/library/windows/hardware/ff539571)父设备目标的属性。

```cpp
WScript.Echo "FriendlyName: " & Device.GetValue("parent/FriendlyName")
```

此外可以合并关系修饰符。 下面的 VBScript 代码示例将的值打印[FriendlyName](https://msdn.microsoft.com/library/windows/hardware/ff539571)的祖父级设备的目标对象的属性。

```cpp
WScript.Echo "FriendlyName: " & Device.GetValue("parent/parent/FriendlyName")
```

有时，设备具有多对多关系。 例如，逻辑存储卷可能驻留在多物理磁盘，并且这些单独的磁盘都可能影响到多个卷的空间。

内 WDTF，所有非接触的虚拟设备 （即以物理方式出现的设备） 是在根设备的后代 (后者可以检索从[ **RootDevice** ](https://msdn.microsoft.com/library/windows/hardware/hh406413)属性)。 (有关虚拟设备的详细信息，请参阅[创建 WDTF 方案](creating-wdtf-scenarios.md)。)

### <a name="collecting-targets-by-using-getrelations"></a>使用 GetRelations 收集目标

如下图所示[ **IWDTFTarget2::GetRelations** ](https://msdn.microsoft.com/library/windows/hardware/hh439400)方法。

![说明 target::getrelations 方法的关系图](images/wdtf-getrelations.gif)

[ **IWDTFTarget2::GetRelations** ](https://msdn.microsoft.com/library/windows/hardware/hh439400)方法接受仅关系说明符一部分 SDEL 语句的语法并返回[ **IWDTFTargets2**](https://msdn.microsoft.com/library/windows/hardware/hh439458)集合接口，其中包含所有满足关系条件的目标。 下面的 VBScript 代码示例返回包含原始目标及其所有同级的集合。

```cpp
Set TestDevices = Device.GetRelations("parent/child/", "")
```

第二个参数[ **GetRelations** ](https://msdn.microsoft.com/library/windows/hardware/hh439400)可以选择性地包含一个语句，传递给[ **Eval** ](https://msdn.microsoft.com/library/windows/hardware/hh439396)方法的每个目标满足的特定关系。 例如，如果您将添加*IsDisableable = true*作为第二个参数，前面的代码示例将返回仅设备，并可禁用其同级。

如果没有任何匹配项，则返回具有零个项的集合。

### <a name="collecting-targets-by-using-query"></a>使用查询收集目标

[ **IWDTFDeviceDepot2** ](https://msdn.microsoft.com/library/windows/hardware/hh406391)接口包含**查询**方法。 此方法采用专为 SDEL 语句[ **IWDTFTarget2::Eval** ](https://msdn.microsoft.com/library/windows/hardware/hh439396)方法，并返回的新实例[ **IWDTFTargets2** ](https://msdn.microsoft.com/library/windows/hardware/hh439458)包含满足查询条件的目标的子集的集合接口。 下面的 VBScript 代码示例枚举所有非接触的虚拟设备，并显示了每个设备的友好名称。

```cpp
For Each Device In WDTF.DeviceDepot.Query("IsPhantom=false")
    WScript.Echo Device.GetValue("FriendlyName")
Next
```

返回的集合具有[ **IWDTFTargets2::Query** ](https://msdn.microsoft.com/library/windows/hardware/hh439483)方法，它具有相同实现到**IWDTFDeviceDepot2::Query**。 **IWDTFTargets2::Query**从原始集合满足 SDEL 语句将返回目标的子集。

### <a name="boolean-logic-in-sdel"></a>在 SDEL 布尔逻辑

[ **IWDTFTarget2::GetRelations** ](https://msdn.microsoft.com/library/windows/hardware/hh439400)方法可以接受仅一个布尔值**或者**运算符，但对调用[ **IWDTFTargets2::查询**](https://msdn.microsoft.com/library/windows/hardware/hh439483)， [ **IWDTFTarget2::Eval**](https://msdn.microsoft.com/library/windows/hardware/hh439396)，以及[ **IWDTFTarget2::GetValue** ](https://msdn.microsoft.com/library/windows/hardware/hh439403)方法可使用布尔值**AND**并**或**运算符。 有关**查询**方法并**Eval**方法中，运算符将处理类似于普通布尔运算符，按预期返回的结果。 但是，对于**GetValue**方法， **AND**将 compose 本身的两面上的值并**或**将返回仅第一个值，它位于 （从左侧开始）。

### <a name="parentheses-in-sdel"></a>括号中 SDEL

所有 SDEL 语句可以都使用括号来指定布尔逻辑的评估顺序。 此外可以在关系或命名空间下一个语句中使用括号将子元素进行分组。

下面的 VBScript 代码示例检索所有卷和子级的祖父级设备。

```cpp
Set Devices = Device.GetRelations("parent/parent/(child/ OR volume/)", "")
```

下面的 VBScript 代码示例检索所有设备都具有多于 1,000,000 字节的可移动介质的子项。

```cpp
Set Devices = WDTF.DeviceDepot.Query("child/disk::(IsRemovable=true AND Size>1000000)")
```

### <a name="sdel-syntax-parsing"></a>SDEL 语法分析

如果将具有语法错误的 SDEL 语句传递给任何 WDTF 中的方法中，该方法将失败，详细的错误信息将返回并解释该问题。

**请注意**  拼写错误的属性、 命名空间或关系令牌不会导致语法错误，因为 SDEL 旨在作为动态基于目标：SDEL 语句必须能够查询动态字段组中的属性存在。

 

 

 




