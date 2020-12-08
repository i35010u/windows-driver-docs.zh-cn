---
title: 编写后操作回调例程
description: 编写后操作回调例程
keywords:
- postoperation 回调例程 WDK 文件系统微筛选器，写入
- 编写回调例程
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6c9b187838a12a04203125b146f92039c9f51246
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96821451"
---
# <a name="writing-postoperation-callback-routines"></a>编写后操作回调例程


## <span id="ddk_writing_postoperation_callback_routines_if"></span><span id="DDK_WRITING_POSTOPERATION_CALLBACK_ROUTINES_IF"></span>


文件系统微筛选器驱动程序使用一个或多个 *postoperation 回调例程* 来筛选 i/o 操作。

Postoperation 回调例程可以执行下列操作之一：

-   直接在 postoperation 例程中完成完成工作。 所有完成工作都可以在 IRQL &lt; = 调度级别完成 \_ 。
-   完成在安全 IRQL 上完成工作。 返回 FLT \_ 状态 \_ 所需的更多 \_ 处理 \_ ，并将工作线程排队以允许在安全的 IRQL 处进行处理。 处理完成后，工作线程将调用 [**FltCompletePendedPostOperation**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcompletependedpostoperation) 以继续 postoperation 处理。
-   取消成功创建操作。

[**Postoperation 回调例程**](/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_post_operation_callback) 与旧式文件系统筛选器驱动程序中使用的 *完成例程* 类似。

微筛选器驱动程序以注册 [**preoperation 回调例程**](/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_pre_operation_callback)的相同方式为特定类型的 i/o 操作注册一个 postoperation 回调例程，即，将回调例程的入口点存储在 [**FLT \_ 注册**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_registration)结构的 **OperationRegistration** 成员中，微筛选器驱动程序将该入口点作为参数 [**传递到 FltRegisterFilter 的**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltregisterfilter) **DriverEntry** 例程中。

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

与完成例程类似， &lt; \_ 在任意线程上下文中，在 IRQL = 调度级别调用 postoperation 回调例程。

由于它可以在 IRQL = 调度级别调用 \_ ，因此 postoperation 回调例程无法调用必须在较低的 IRQL （例如 [**FltLockUserBuffer**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltlockuserbuffer) 或 [**RtlCompareUnicodeString**](/windows-hardware/drivers/ddi/wdm/nf-wdm-rtlcompareunicodestring)）中调用的内核模式例程。 由于同样的原因，在 postoperation 回调例程中使用的所有数据结构必须从非分页池进行分配。

以下情况是上述规则的几个例外：

-   如果微筛选器驱动程序的 preoperation 回调例程 \_ \_ 为基于 IRP 的 i/o 操作返回 FLT PREOP 同步，则会在与 &lt; \_ preoperation 回调例程相同的线程上下文中调用相应的 postoperation 回调例程，该例程在 IRQL = APC 级别。

-   快速 i/o 操作的 postoperation 回调例程在与 \_ preoperation 回调例程相同的线程上下文中的 IRQL = 被动级别调用。

-   \_在源自 IRP \_ MJ create 操作的线程的上下文中，在 IRQL = 被动级别调用创建后回调例程 \_ 。

当筛选器管理器为给定 i/o 操作调用微筛选器驱动程序的 postoperation 回调例程时，微筛选器驱动程序会暂时控制 i/o 操作。 微筛选器驱动程序会保留此控件，直到它执行以下操作之一：

-   \_ \_ 从 postoperation 回调例程返回 FLT POSTOP 已完成 \_ 处理。

-   从已处理基于 IRP 的 i/o 操作的工作例程调用 [**FltCompletePendedPostOperation**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcompletependedpostoperation) ，该操作已在 postoperation 回调例程中挂起。

本节包括：

[执行 i/o 操作的完成处理](performing-completion-processing-for-an-i-o-operation.md)

[挂起 Postoperation 回调例程中的 i/o 操作](pending-an-i-o-operation-in-a-postoperation-callback-routine.md)

[Postoperation 回调例程中的 i/o 操作失败](failing-an-i-o-operation-in-a-postoperation-callback-routine.md)

 

