---
title: C28169
description: 警告 C28169 调度函数没有任何 _Dispatch_type_ 注释。
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28169
ms.openlocfilehash: bdb0d827c9bd189333ded03a049dfce100d5689e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838157"
---
# <a name="c28169"></a>C28169


警告 C28169：调度函数没有任何 **\_ 调度 \_ 类型 \_** 批注

当对 **MajorFunction** 表赋值的右侧没有 (有效) **\_ 调度 \_ 类型 \_** 注释时，代码分析工具将报告此警告。 如果右侧的强制转换去除了 **\_ 派单 \_ 类型 \_** 注释，有时会出现警告。 右侧应为类型为 "驱动程序" 的函数 \_ ，并且具有适当的 **\_ 调度 \_ 类型 \_** 批注。

有关详细信息，请参阅 [使用函数角色类型声明](using-function-role-type-declarations.md)。

### <a name="span-idexamplespanspan-idexamplespanexample"></a><span id="example"></span><span id="EXAMPLE"></span>示例

如果在 **MajorFunction** 的调度例程分配中使用函数，则以下函数声明 elicits 此警告。

```
NTSTATUS
DispatchSystemControl (
    PDEVICE_OBJECT  DeviceObject,
    PIRP            Irp
    );
```

以相同方式使用的以下函数声明不会得出此警告。

```
// Function: DispatchSystemControl
// This is an example of a fully annotated declaration.  
// IRP_MJ_SYSTEM_CONTROL is the type of IRP handled by this function.  
// Multiple _Dispatch_type_ lines are acceptable if the function handles more than 1 IRP type.
//
_Dispatch_type_(IRP_MJ_SYSTEM_CONTROL) 
DRIVER_DISPATCH DispatchSystemControl;
```

 

 





