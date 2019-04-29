---
title: C28169
description: 警告 C28169 调度函数没有任何_Dispatch_type_批注。
ms.assetid: ce33993f-f967-43b0-89fb-d8553517aae3
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28169
ms.openlocfilehash: 18719142bb32fd32fada4cdd8db479d3c112ab1f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63361462"
---
# <a name="c28169"></a>C28169


警告 C28169:调度函数没有任何**\_调度\_类型\_** 批注

代码分析工具将报告此警告向赋值的右侧**MajorFunction**表中没有 （有效） **\_调度\_类型\_** 批注。 警告有时会剥离的强制转换的右侧是否**\_调度\_类型\_** 批注。 在右侧应为类型驱动程序的函数\_调度类型使用相应**\_调度\_类型\_** 批注。

有关详细信息，请参阅[使用函数角色类型声明](using-function-role-type-declarations.md)。

### <a name="span-idexamplespanspan-idexamplespanexample"></a><span id="example"></span><span id="EXAMPLE"></span>示例

以下函数声明会引起此警告，如果该函数使用中的调度例程分配**MajorFunction**。

```
NTSTATUS
DispatchSystemControl (
    PDEVICE_OBJECT  DeviceObject,
    PIRP            Irp
    );
```

以下函数声明中，使用方式相同，不引发此警告。

```
// Function: DispatchSystemControl
// This is an example of a fully annotated declaration.  
// IRP_MJ_SYSTEM_CONTROL is the type of IRP handled by this function.  
// Multiple _Dispatch_type_ lines are acceptable if the function handles more than 1 IRP type.
//
_Dispatch_type_(IRP_MJ_SYSTEM_CONTROL) 
DRIVER_DISPATCH DispatchSystemControl;
```

 

 





