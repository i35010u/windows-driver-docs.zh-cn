---
title: 简单数据评估语言概述
description: WDTF 包括一个简单的查询语言，用于简化基于属性或关系收集目标的任务。
ms.assetid: 84c2a1d6-6bec-4aeb-b858-c29f50d74390
keywords:
- Windows 设备测试框架 WDK，SDEL
- WDTF WDK，SDEL
- 简单数据评估语言 WDK WDTF
- SDEL WDK WDTF
- 查询语言 WDK WDTF
- 目标对象 WDK WDTF
- 命名空间 WDK WDTF
- 基于关系的测试 WDK WDTF
- 关系说明符 WDK WDTF
- 命名查询 WDK WDTF
- 属性 WDK WDTF
- 布尔逻辑 WDK WDTF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 16284065f9defca13539bf85c36957041b1fa48d
ms.sourcegitcommit: bd72676caf2bf5c9738c4081c778316919b85d30
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2020
ms.locfileid: "89450200"
---
# <a name="simple-data-evaluation-language-overview"></a>简单数据评估语言概述

WDTF 包括一个简单的查询语言，用于简化基于属性或关系收集目标的任务。 简单的数据计算语言 (SDEL) 与 XPath 类似。 有关 XPath 的详细信息，请参阅 [Xpath 参考](https://go.microsoft.com/fwlink/p/?linkid=33165)。

本主题中的以下部分介绍了如何使用 SDEL。

>[!NOTE]
>有关所有命名空间令牌及其内部的属性令牌的完整列表，请参阅 [SDEL 中的设备关系令牌](device-relation-tokens-in-sdel.md) 和 SDEL 中的 [属性标记](attribute-tokens-in-sdel.md)。

## <a name="sdel-syntax-basics"></a>SDEL 语法基础知识

SDEL 使用特性标记执行匹配和检索数据。 所有 SDEL 令牌只能包含字母数字字符和连字符， ( ) 。

*特性*是指附加到目标的一段数据。 特性中的实际值将存储为 **变量**。 如果在属性后放置比较运算符后跟一个 *测试* 值，则 SDEL 将执行比较匹配。 应将测试值放在单引号或双引号中--此表示法允许在测试值中使用实际的单引号或双引号，但不能同时使用这两者。 如果测试值仅包含字母数字字符和连字符 ( ) ，则可以省略引号。

### <a name="comparison-operations"></a>比较运算

SDEL 允许各种比较运算符遵循属性标记。 在进行比较时，运算符左侧属性中的实际值通过 **VariantChangeType** 方法与运算符右侧的测试值的类型相同， (该方法在 Microsoft Windows SDK 文档) 中进行了介绍。 下表显示了 SDEL 支持的不同比较运算符。

比较运算符意味着相等性 (=) 

更改类型后，将使用 **VarCmp** 方法对它们进行比较， (这在 Windows SDK 文档) 中进行了介绍。

不等于 (！ =) 

小于号 (&lt;)

小于等于 (&lt; =) 

大于 (&gt;) 

大于或等于 (&gt; =) 

按位“与”(&)

在对 \_ 实际值和测试值执行按位 "与" 运算之前，该运算符会将类型强制转换为 VT I8。

没有 (比较运算，并且未指定任何值) 

如果属性中的实际值为 VT \_ BOOL 类型，则根据该值满足匹配项，也就是说，不需要比较运算符即可执行 "IsDisableable = True"。 否则，如果除 VT 空) 之外的任何 (都有任何值 \_ ，则满足匹配。

如果在属性中有多个实际值 (或数组) ，则所有比较运算符都应解释为至少匹配一个，但不相等运算符，后者具有相反的行为。 如果在所有 (都不能比较类型，则 **VariantChangeType** 将失败) ，除了不相等运算符之外，不存在任何匹配 (，后者的行为) 相反。

### <a name="understanding-attribute-namespaces"></a>了解属性命名空间

SDEL 使用命名空间令牌对属性进行分组。 有关所有命名空间令牌及其内部的属性令牌的完整列表，请参阅 [SDEL 中的属性标记](attribute-tokens-in-sdel.md)。

若要使用根命名空间之外的任何属性，必须将属性作为命名空间名称的前缀，然后使用两个冒号 (：： ) 。 以下 VBScript 代码示例显示 Disk：： IsRemovable 特性的值。

```cpp
WScript.Echo "Is Removable?: " & DeviceObj.GetValue("Disk::IsRemovable")
```

### <a name="examining-a-target-by-using-getvalue-and-eval"></a>使用 GetValue 和 Eval 检查目标

使用 [**IWDTFTarget2：： GetValue**](/windows-hardware/drivers/ddi/wdtf/nf-wdtf-iwdtftarget2-getvalue) 方法，你可以向目标询问其特性。 下面的 VBScript 代码示例打印目标的 [FriendlyName](attribute-tokens-in-sdel.md#root-attribute-tokens-for-a-device-target) 特性的值。

```cpp
WScript.Echo "FriendlyName: " & Device.GetValue("FriendlyName")
```

有关属性标记的完整列表，请参阅 [SDEL 中的属性标记](attribute-tokens-in-sdel.md)。

还可以使用 [**IWDTFTarget2：： Eval**](/windows-hardware/drivers/ddi/wdtf/nf-wdtf-iwdtftarget2-eval) 方法针对目标计算 SDEL 语句。 **Eval** 返回 **变体 \_ TRUE** 或 **变体 \_ FALSE**。 下面的 VBScript 代码示例使用 **Eval** 确定是否可以禁用设备。

```cpp
If Device.Eval("IsDisableable=true") Then
    WScript.Echo "Target is disableable!"
End If
```

你还可以使用 [**Eval**](/windows-hardware/drivers/ddi/wdtf/nf-wdtf-iwdtftarget2-eval) 测试属性是否存在。 当您传递**Eval**而不是比较运算符或值时，如果特性或命名空间包含除**VT \_ 空**) 以外的任何 (值，则**eval**将返回**变体 \_ TRUE** 。 下面的 VBScript 代码示例使用 **Eval** 确定目标是否具有 SymbolicLink 关键字。

```cpp
If Device.Eval("SymbolicLink") Then
    WScript.Echo "Target has a SymbolicLink!"
End If
```

此外，缺少比较运算符但包含 **VT \_ BOOL** 值的属性将对其应用隐式 "= true" 比较。 此隐式比较意味着 "IsDisableable" 等效于 "IsDisableable = ' true '"。

## <a name="navigating-relationships"></a>导航关系

测试通常涉及到检查相关设备更改状态时所发生的情况。 例如，当 USB 集线器处于禁用状态时，附加到它的设备是否能正确处理状态更改？ 此外，您可能还需要根据相关设备中的信息查找设备。 为了支持此功能，SDEL 包含了一种在任何属性或命名空间 (之前指定一个或多个逻辑关系的方法，但不能) 。 关系标记通过正斜杠 (/) 与特性或命名空间分隔。 下面的 VBScript 代码示例打印目标父设备的 [FriendlyName](attribute-tokens-in-sdel.md#root-attribute-tokens-for-a-device-target) 特性的值。

```cpp
WScript.Echo "FriendlyName: " & Device.GetValue("parent/FriendlyName")
```

您还可以组合关系修饰符。 下面的 VBScript 代码示例打印目标对象的祖父设备的 [FriendlyName](attribute-tokens-in-sdel.md#root-attribute-tokens-for-a-device-target) 特性的值。

```cpp
WScript.Echo "FriendlyName: " & Device.GetValue("parent/parent/FriendlyName")
```

有时，设备具有多对多关系。 例如，逻辑存储卷可能驻留在多个物理磁盘上，而这些单独的磁盘可能会为多个卷提供空间。

在 WDTF 中，所有非虚拟设备 (即，在物理上存在的设备) 是根设备 (的后代，你可以从 [**RootDevice**](/windows-hardware/drivers/ddi/wdtf/nf-wdtf-iwdtfdevicedepot2-get_rootdevice) 属性) 检索。  (有关虚拟设备的详细信息，请参阅 [创建 WDTF 方案](creating-wdtf-scenarios.md)。 ) 

## <a name="collecting-targets-by-using-getrelations"></a>使用 GetRelations 收集目标

下图显示了 [**IWDTFTarget2：： GetRelations**](/windows-hardware/drivers/ddi/wdtf/nf-wdtf-iwdtftarget2-getrelations) 方法。

![说明 target：： getrelations 方法的关系图](images/wdtf-getrelations.gif)

[**IWDTFTarget2：： GetRelations**](/windows-hardware/drivers/ddi/wdtf/nf-wdtf-iwdtftarget2-getrelations)方法仅接受 SDEL 语句语法的关系说明符部分，并返回一个[**IWDTFTargets2**](/windows-hardware/drivers/ddi/wdtf/nn-wdtf-iwdtftargets2)集合接口，其中包含满足关系条件的所有目标。 下面的 VBScript 代码示例返回一个集合，其中包含原始目标及其所有同级。

```cpp
Set TestDevices = Device.GetRelations("parent/child/", "")
```

[**GetRelations**](/windows-hardware/drivers/ddi/wdtf/nf-wdtf-iwdtftarget2-getrelations)的第二个参数可以有选择性地包含要传递给满足特定关系的每个目标的[**Eval**](/windows-hardware/drivers/ddi/wdtf/nf-wdtf-iwdtftarget2-eval)方法的语句。 例如，如果将 *IsDisableable = true* 添加为第二个参数，则上面的代码示例将仅返回可禁用的设备及其同级。

如果没有匹配项，则返回包含零项的集合。

## <a name="collecting-targets-by-using-query"></a>使用查询收集目标

[**IWDTFDeviceDepot2**](/windows-hardware/drivers/ddi/wdtf/nn-wdtf-iwdtfdevicedepot2)接口包含一个**查询**方法。 此方法采用为 [**IWDTFTarget2：： Eval**](/windows-hardware/drivers/ddi/wdtf/nf-wdtf-iwdtftarget2-eval) 方法设计的 SDEL 语句，并返回 [**IWDTFTargets2**](/windows-hardware/drivers/ddi/wdtf/nn-wdtf-iwdtftargets2) 集合接口的新实例，该实例包含符合查询条件的目标的子集。 以下 VBScript 代码示例列举了所有非虚拟设备，并显示了每个设备的友好名称。

```cpp
For Each Device In WDTF.DeviceDepot.Query("IsPhantom=false")
    WScript.Echo Device.GetValue("FriendlyName")
Next
```

返回的集合包含 [**IWDTFTargets2：： query**](/windows-hardware/drivers/ddi/wdtf/nf-wdtf-iwdtftargets2-query) 方法，该方法具有与 **IWDTFDeviceDepot2：： query**相同的实现。 **IWDTFTargets2：： Query** 从满足 SDEL 语句的原始集合返回目标的子集。

## <a name="boolean-logic-in-sdel"></a>SDEL 中的布尔逻辑

[**IWDTFTarget2：： GetRelations**](/windows-hardware/drivers/ddi/wdtf/nf-wdtf-iwdtftarget2-getrelations)方法只能接受布尔值**或**运算符，但对[**IWDTFTargets2：： Query**](/windows-hardware/drivers/ddi/wdtf/nf-wdtf-iwdtftargets2-query)、 [**IWDTFTarget2：： Eval**](/windows-hardware/drivers/ddi/wdtf/nf-wdtf-iwdtftarget2-eval)和[**IWDTFTarget2：： GetValue**](/windows-hardware/drivers/ddi/wdtf/nf-wdtf-iwdtftarget2-getvalue)方法的调用可以使用 boolean**和**and **OR**运算符。 对于 **查询** 方法和 **Eval** 方法，运算符的作用类似于常规布尔运算符，并按预期返回结果。 但是，对于 **GetValue** 方法， **并** 将在其自身的两侧组合值， **或** 将仅返回从左) 开始 (找到的第一个值。

## <a name="parentheses-in-sdel"></a>SDEL 中的括号

所有 SDEL 语句都可以使用括号来指定布尔逻辑的计算序列。 你还可以使用括号对关系或命名空间下的语句中的子元素进行分组。

下面的 VBScript 代码示例检索祖父设备的所有卷和子节点。

```cpp
Set Devices = Device.GetRelations("parent/parent/(child/ OR volume/)", "")
```

下面的 VBScript 代码示例检索具有大于1000000字节的可移动媒体的子的所有设备。

```cpp
Set Devices = WDTF.DeviceDepot.Query("child/disk::(IsRemovable=true AND Size>1000000)")
```

## <a name="sdel-syntax-parsing"></a>SDEL 语法分析

如果将具有错误语法的 SDEL 语句传递到 WDTF 中的任何方法，则该方法将失败，并将返回详细的错误信息，并解释此问题。

>[!NOTE]
>拼写错误的特性、命名空间或关系标记不会导致语法错误，因为 SDEL 设计为基于目标的动态： SDEL 语句必须能够查询动态字段集中是否存在属性。
