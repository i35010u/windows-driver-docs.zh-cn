---
title: 编写后操作回调例程
description: 编写后操作回调例程
ms.assetid: 4940e38d-107b-45c4-aa71-6e8543330f39
keywords:
- postoperation 回调例程 WDK 文件系统微筛选器、 编写
- 编写回调例程
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7fb1e5ca4d47cd98c0f40d13098cdd19b37bee55
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63367111"
---
# <a name="writing-postoperation-callback-routines"></a>编写后操作回调例程


## <span id="ddk_writing_postoperation_callback_routines_if"></span><span id="DDK_WRITING_POSTOPERATION_CALLBACK_ROUTINES_IF"></span>


文件系统微筛选器驱动程序使用一个或多个*postoperation 回调例程*到筛选器 I/O 的操作。

Postoperation 回调例程可以执行以下操作之一：

-   完成 postoperation 例程中直接完成工作。 所有完成的工作都可以在 IRQL &lt;= 调度\_级别。
-   完成安全 IRQL 在完成工作。 返回 FLT\_状态\_详细\_处理\_必需和队列工作线程，以允许在安全的 IRQL 在处理。 处理完成后，工作线程调用[ **FltCompletePendedPostOperation** ](https://msdn.microsoft.com/library/windows/hardware/ff541897)继续 postoperation 处理。
-   取消成功创建操作。

[**Postoperation 回调例程**](https://msdn.microsoft.com/library/windows/hardware/ff551107)类似于*完成例程*在旧的文件系统筛选器驱动程序中使用。

微筛选器驱动程序与它注册相同的方式注册特定类型的 I/O 操作的 postoperation 回调例程[ **preoperation 回调例程**](https://msdn.microsoft.com/library/windows/hardware/ff551109)— 也就是说，通过存储回调中的例程的入口点**OperationRegistration**的成员[ **FLT\_注册**](https://msdn.microsoft.com/library/windows/hardware/ff544811)微筛选器驱动程序将传递的结构为参数[ **FltRegisterFilter** ](https://msdn.microsoft.com/library/windows/hardware/ff544305)中其**DriverEntry**例程。

微筛选器驱动程序收到只有这些类型的 I/O 操作，它们具有为其注册 preoperation 或 postoperation 回调例程。 微筛选器驱动程序可以注册为给定类型的 I/O 操作的 preoperation 回调例程，而不注册 postoperation 回调，反之亦然。

每个 postoperation 回调例程定义，如下所示：

```cpp
typedef FLT_POSTOP_CALLBACK_STATUS 
(*PFLT_POST_OPERATION_CALLBACK) ( 
    IN OUT PFLT_CALLBACK_DATA Data, 
    IN PCFLT_RELATED_OBJECTS FltObjects, 
    IN PVOID CompletionContext, 
    IN FLT_POST_OPERATION_FLAGS Flags 
    ); 
```

完成例程，如在 IRQL 调用 postoperation 回调例程&lt;= 调度\_级别，请在任意线程上下文中。

因为它可以调用在 IRQL = 调度\_级别，postoperation 回调例程不能调用必须在较低的 IRQL，如调用的内核模式例程[ **FltLockUserBuffer** ](https://msdn.microsoft.com/library/windows/hardware/ff543371)或[ **RtlCompareUnicodeString**](https://msdn.microsoft.com/library/windows/hardware/ff561782)。 出于相同原因，必须从非分页缓冲池分配 postoperation 回调例程中使用任何数据结构。

在以下情况下是上述规则的几个例外情况：

-   如果微筛选器驱动程序的 preoperation 回调例程将返回 FLT\_PREOP\_IRP 基于 I/O 操作，相应的 postoperation 回调例程的同步调用在 IRQL &lt;= APC\_级别，在 preoperation 回调例程在同一线程上下文。

-   快速的 I/O 操作的 postoperation 回调例程调用在 IRQL = 被动\_级别，请在 preoperation 回调例程在同一线程上下文中。

-   在 IRQL 调用后创建的回调例程 = 被动\_级别，请在发起 IRP 的线程的上下文\_MJ\_创建操作。

当筛选器管理器调用指定的 I/O 操作时微筛选器驱动程序的 postoperation 回调例程时，微筛选器驱动程序将暂时控制 I/O 操作。 微筛选器驱动程序将保留此控件，直到它执行以下项之一：

-   返回 FLT\_POSTOP\_已完成\_处理从 postoperation 回调例程。

-   调用[ **FltCompletePendedPostOperation** ](https://msdn.microsoft.com/library/windows/hardware/ff541897)从已处理被挂起 postoperation 回调例程中的基于 IRP 的 I/O 操作的工作例程。

本部分包括：

[执行完成某个 I/O 操作的处理](performing-completion-processing-for-an-i-o-operation.md)

[挂起的 I/O 操作中 Postoperation 回调例程](pending-an-i-o-operation-in-a-postoperation-callback-routine.md)

[失败的 I/O 操作中 Postoperation 回调例程](failing-an-i-o-operation-in-a-postoperation-callback-routine.md)

 

 




