---
title: 编写后操作回调例程
description: 编写后操作回调例程
ms.assetid: 4940e38d-107b-45c4-aa71-6e8543330f39
keywords:
- postoperation 回调例程 WDK 文件系统微筛选器，写入
- 编写回调例程
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 22a41557c7994e7cf5ac38da43fb858c7c7a08f1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840921"
---
# <a name="writing-postoperation-callback-routines"></a>编写后操作回调例程


## <span id="ddk_writing_postoperation_callback_routines_if"></span><span id="DDK_WRITING_POSTOPERATION_CALLBACK_ROUTINES_IF"></span>


文件系统微筛选器驱动程序使用一个或多个*postoperation 回调例程*来筛选 i/o 操作。

Postoperation 回调例程可以执行下列操作之一：

-   直接在 postoperation 例程中完成完成工作。 所有完成工作都可以在 IRQL 上完成，&lt;= 调度\_级别。
-   完成在安全 IRQL 上完成工作。 返回 FLT\_状态\_详细\_处理\_必需，并将工作线程排队以允许在安全的 IRQL 处进行处理。 处理完成后，工作线程将调用[**FltCompletePendedPostOperation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcompletependedpostoperation)以继续 postoperation 处理。
-   取消成功创建操作。

[**Postoperation 回调例程**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_post_operation_callback)与旧式文件系统筛选器驱动程序中使用的*完成例程*类似。

微筛选器驱动程序以注册[**preoperation 回调例程**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_pre_operation_callback)的相同方式为特定类型的 i/o 操作注册一个 postoperation 回调例程，即通过将回调例程的入口点存储在 OperationRegistration 中。 [**FLT\_注册**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_registration)结构的成员，微筛选器驱动程序将其作为参数传递给**DriverEntry**例程中的[**FltRegisterFilter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltregisterfilter) 。

微筛选器驱动程序只接收到其已为其注册 preoperation 或 postoperation 回调例程的 i/o 操作类型。 微筛选器驱动程序可以为给定类型的 i/o 操作注册一个 preoperation 回调例程，而无需注册 postoperation 回调，反之亦然。

每个 postoperation 回调例程定义如下：

```cpp
typedef FLT_POSTOP_CALLBACK_STATUS 
(*PFLT_POST_OPERATION_CALLBACK) ( 
    IN OUT PFLT_CALLBACK_DATA Data, 
    IN PCFLT_RELATED_OBJECTS FltObjects, 
    IN PVOID CompletionContext, 
    IN FLT_POST_OPERATION_FLAGS Flags 
    ); 
```

与完成例程一样，postoperation 回调例程在任意线程上下文中以 IRQL &lt;= 调度\_级别调用。

由于它可以在 IRQL = 调度\_级别调用，因此 postoperation 回调例程无法调用必须在较低的 IRQL （例如[**FltLockUserBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltlockuserbuffer)或[**RtlCompareUnicodeString**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-rtlcompareunicodestring)）上调用的内核模式例程。 由于同样的原因，在 postoperation 回调例程中使用的所有数据结构必须从非分页池进行分配。

以下情况是上述规则的几个例外：

-   如果微筛选器驱动程序的 preoperation 回调例程返回 FLT\_PREOP\_为基于 IRP 的 i/o 操作同步，则会在同一线程中以 IRQL &lt;= APC\_级别调用相应的 postoperation 回调例程上下文作为 preoperation 回调例程。

-   快速 i/o 操作的 postoperation 回调例程在 preoperation 回调例程所在的线程上下文中以 IRQL = 被动\_级别调用。

-   在发起 IRP\_MJ\_创建操作的线程的上下文中，在 IRQL = 被动\_级别调用创建后回调例程。

当筛选器管理器为给定 i/o 操作调用微筛选器驱动程序的 postoperation 回调例程时，微筛选器驱动程序会暂时控制 i/o 操作。 微筛选器驱动程序会保留此控件，直到它执行以下操作之一：

-   从 postoperation 回调例程返回 FLT\_POSTOP\_完成\_处理。

-   从已处理基于 IRP 的 i/o 操作的工作例程调用[**FltCompletePendedPostOperation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcompletependedpostoperation) ，该操作已在 postoperation 回调例程中挂起。

本部分包括：

[执行 i/o 操作的完成处理](performing-completion-processing-for-an-i-o-operation.md)

[挂起 Postoperation 回调例程中的 i/o 操作](pending-an-i-o-operation-in-a-postoperation-callback-routine.md)

[Postoperation 回调例程中的 i/o 操作失败](failing-an-i-o-operation-in-a-postoperation-callback-routine.md)

 

 




