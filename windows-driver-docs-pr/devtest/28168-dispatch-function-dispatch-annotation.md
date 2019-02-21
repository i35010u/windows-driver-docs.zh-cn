---
title: C28168
description: 调度函数没有警告 C28168 _Dispatch_type_批注匹配此调度表条目。
ms.assetid: 5e5acc54-acb3-4366-a625-eb79865e932e
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28168
ms.openlocfilehash: b0193771152d701e04b3e39a3bd0586079099a5b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542477"
---
# <a name="c28168"></a>C28168


警告 C28168:调度函数没有**\_调度\_类型\_** 批注匹配此调度表条目

此警告支持[Static Driver Verifier](static-driver-verifier.md)通过检查到调度表分配每个函数将以一个或多个批注**\_调度\_类型\_** 指示的由该函数执行的调度操作的类型的批注。 针对函数的批注不匹配的调度表项槽时，代码分析工具将报告此错误。

可以通过添加可更正此缺陷**\_调度\_类型\_** 批注相对于函数或更正所使用的调度表项。

### <a name="span-idexamplespanspan-idexamplespanexample"></a><span id="example"></span><span id="EXAMPLE"></span>示例

下面的代码示例将生成此警告。

```
DRIVER_DISPATCH SampleCreate;
...
pDo->MajorFunction[IRP_MJ_CREATE] = SampleCreate;
...
```

下面的代码示例可避免此警告。

```
_Dispatch_type_(IRP_MJ_CREATE) DRIVER_DISPATCH SampleCreate;
...
pDo->MajorFunction[IRP_MJ_CREATE] = SampleCreate;
...
```

## <a name="span-idcommentsspanspan-idcommentsspanspan-idcommentsspancomments"></a><span id="Comments"></span><span id="comments"></span><span id="COMMENTS"></span>注释


在某些情况下，可能需要禁止显示此警告。 有一些驱动程序，例如，筛选器驱动程序后直接注册其他人, 可能注册在一个循环内的调度例程。

```ManagedCPlusPlus
DriverObject->MajorFunction[IRP_MJ_CREATE]         = DispatchCreate;
DriverObject->MajorFunction[IRP_MJ_READ]           = DispatchRead;
for (Index = 0; Index <= IRP_MJ_MAXIMUM_FUNCTION; Index++)
    {
            DriverObject->MajorFunction[Index] = DispatchPassIrp;
    }
```

在此示例中， **DispatchPassIrp**使用下列批注正确声明函数：

```ManagedCPlusPlus
__drv_dispatchType(IRP_MJ_CREATE_NAMED_PIPE)
__drv_dispatchType(IRP_MJ_QUERY_INFORMATION)
// .... 
//  (additional dispatch type annotations) 
// ....
__drv_dispatchType(IRP_MJ_CREATE_NAMED_PIPE)
    DRIVER_DISPATCH DispatchPassIrp;
```

在此情况下，代码分析工具将报告此错误：

```
The function 'DispatchPassIrp' does not have a _Dispatch_type_ annotation matching dispatch table position 'IRP_MJ_CREATE' (0x00):  This can be  corrected either by adding a _Dispatch_type_ annotation to the function declaration or correcting the dispatch table entry being used.
```

在某些筛选器驱动程序中常见的调度表中的循环这种用法。 在此情况下，可以忽略该错误消息，因为这是静态分析的限制。 针对函数的批注不匹配的调度表项槽时，代码分析工具将报告此错误。 在这种情况下，代码分析工具将报告非法赋值 (的撤消了更高版本)。 但是，没有更高版本的一个静态工具，可知道，将撤消非法状态的方法。 如果您知道要进行分配，这样一来，并带来更高版本，则可以禁止显示警告。

 

 





