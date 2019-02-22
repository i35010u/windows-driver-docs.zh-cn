---
title: 使用驱动程序定义的回调对象
description: 使用驱动程序定义的回调对象
ms.assetid: b3b32534-0641-4818-9384-65fd45f689e8
keywords:
- 回调对象 WDK 内核
- 驱动程序定义的回调对象 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8a28711ec8958f9dc14e8884e946f153de2dd6ab
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522899"
---
# <a name="using-a-driver-defined-callback-object"></a>使用驱动程序定义的回调对象





若要使用另一个驱动程序定义的回调对象，驱动程序打开对象，然后注册一个例程调用触发回调后下, 图中所示。 驱动程序请求通知必须知道的回调对象的名称，并且必须了解传递给回调例程的参数的语义。

![说明的回调通知注册的关系图](images/3reg-cbk.png)

它可以打开的对象之前，该驱动程序必须调用[ **InitializeObjectAttributes** ](https://msdn.microsoft.com/library/windows/hardware/ff547804)创建特性块，指定的对象的名称。 它具有到特性块的指针后，它会调用[ **ExCreateCallback**](https://msdn.microsoft.com/library/windows/hardware/ff544560)，并传递属性指针，在其中以接收回调的句柄的位置和**FALSE**对于*创建*参数，指示它需要一个现有的回调对象。

然后，该驱动程序可以调用[ **ExRegisterCallback** ](https://msdn.microsoft.com/library/windows/hardware/ff545534)与返回的句柄来注册其回调例程。

回调例程具有以下原型：

```cpp
typedef VOID (*PCALLBACK_FUNCTION ) (
    IN PVOID CallbackContext,
    IN PVOID Argument1,
    IN PVOID Argument2
    );
```

*CallbackContext*参数是要传递给回调例程每次调用它的上下文指针。 通常情况下，此参数是指向调用方应从非分页缓冲池分配，如果可以在调度调用例程的上下文数据的块的\_级别。 创建回调的组件定义了两个参数。 通常情况下，自变量提供有关触发回调的条件的信息。

当回调触发器通知的创建者，系统调用的已注册的例程，将指针传递到上下文和两个参数。 创建回调的组件提供的自变量的值。 在创建驱动程序触发通知，这始终是 IRQL 相同 IRQL 调用回调例程&lt;= 调度\_级别。

在其回调例程，驱动程序可以执行它需要使用的当前条件的任何任务。

当驱动程序不再需要通知时，则应调用[ **ExUnregisterCallback** ](https://msdn.microsoft.com/library/windows/hardware/ff545649)若要从已注册的回调的列表中删除其例程并删除其对回调对象的引用。

 

 




