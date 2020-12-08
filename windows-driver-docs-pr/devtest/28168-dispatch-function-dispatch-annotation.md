---
title: C28168
description: 警告 C28168 调度函数没有与此调度表项匹配的 _Dispatch_type_ 注释。
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28168
ms.openlocfilehash: 7c78faf01d7352137abcc91fe8aad184d04c9e0d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838159"
---
# <a name="c28168"></a>C28168


警告 C28168：调度函数没有与此调度表项匹配的 **\_ 调度 \_ 类型 \_** 批注

此警告支持 [静态驱动程序验证程序](static-driver-verifier.md)，方法是检查分配给调度表的每个函数是否使用一个或多个 **\_ 调度 \_ 类型 \_** 批注（指示该函数执行的调度操作的类型）进行批注。 当函数上的批注与调度表条目槽不匹配时，代码分析工具将报告此错误。

可以通过向函数添加 **\_ 调度 \_ 类型 \_** 注释或更正所使用的调度表项来更正此缺陷。

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

## <a name="span-idcommentsspanspan-idcommentsspanspan-idcommentsspancomments"></a><span id="Comments"></span><span id="comments"></span><span id="COMMENTS"></span>提出


在某些情况下，可能需要禁止显示此警告。 有些驱动程序（例如筛选器驱动程序）可以在循环中注册调度例程，然后再直接注册其他驱动程序。

```ManagedCPlusPlus
DriverObject->MajorFunction[IRP_MJ_CREATE]         = DispatchCreate;
DriverObject->MajorFunction[IRP_MJ_READ]           = DispatchRead;
for (Index = 0; Index <= IRP_MJ_MAXIMUM_FUNCTION; Index++)
    {
            DriverObject->MajorFunction[Index] = DispatchPassIrp;
    }
```

在此示例中， **DispatchPassIrp** 函数已由以下注释正确声明：

```ManagedCPlusPlus
__drv_dispatchType(IRP_MJ_CREATE_NAMED_PIPE)
__drv_dispatchType(IRP_MJ_QUERY_INFORMATION)
// .... 
//  (additional dispatch type annotations) 
// ....
__drv_dispatchType(IRP_MJ_CREATE_NAMED_PIPE)
    DRIVER_DISPATCH DispatchPassIrp;
```

在这种情况下，代码分析工具将报告此错误：

```
The function 'DispatchPassIrp' does not have a _Dispatch_type_ annotation matching dispatch table position 'IRP_MJ_CREATE' (0x00):  This can be  corrected either by adding a _Dispatch_type_ annotation to the function declaration or correcting the dispatch table entry being used.
```

此在调度表中使用循环在某些筛选器驱动程序中很常见。 在这种情况下，可以忽略错误消息，因为这是静态分析的限制。 当函数上的批注与调度表条目槽不匹配时，代码分析工具将报告此错误。 在这种情况下，代码分析工具将报告一个非法赋值 (，稍后将其) 撤消。 但是，静态工具没有办法知道稍后将撤消非法状态。 如果你知道你是以这种方式进行分配，并稍后修复它们，则可以禁止显示此警告。

 

 





