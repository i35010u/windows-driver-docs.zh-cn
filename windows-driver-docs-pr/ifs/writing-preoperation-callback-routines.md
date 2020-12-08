---
title: 编写预操作回调例程
description: 编写预操作回调例程
keywords:
- preoperation 回调例程 WDK 文件系统微筛选器，写入
- 编写回调例程
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 27a930ad5c32f151aa5d6cb67ff88f5492342f0e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96832995"
---
# <a name="writing-preoperation-callback-routines"></a>编写预操作回调例程


## <span id="ddk_writing_preoperation_callback_routines_if"></span><span id="DDK_WRITING_PREOPERATION_CALLBACK_ROUTINES_IF"></span>


文件系统微筛选器驱动程序使用一个或多个 *preoperation 回调例程* 来筛选 i/o 操作。 [**Preoperation 回调例程**](/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_pre_operation_callback) 类似于在旧式文件系统筛选器驱动程序中使用的调度例程。

微筛选器驱动程序通过将回调例程的入口点存储在 [**FLT \_ 注册**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_registration)结构的 **OperationRegistration** 成员中，为特定类型的 i/o 操作注册一个 preoperation 回调例程。 微筛选器驱动程序将此成员作为参数传递到其 **DriverEntry** 例程中的 [**FltRegisterFilter**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltregisterfilter) 。

微筛选器驱动程序只接收到其已为其注册 preoperation 或 postoperation 回调例程的 i/o 操作类型。 微筛选器驱动程序可以为给定类型的 i/o 操作注册一个 preoperation 回调例程，而无需注册 [**postoperation 回调例程**](/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_post_operation_callback)，反之亦然。

下表显示了特定使用方案的 preoperation 回调例程实现及其返回值。

| 使用方案                                                                                                                                                                        | 实现                                                                                                                                       | 返回的值                      |
|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------|
| 例程与操作无关，无需操作的最终状态或它没有 postoperation 回调。                                             | 传递 i/o 操作，而无需在完成时调用微筛选器的 postoperation 回调。                                                | FLT \_ PREOP \_ SUCCESS \_ 无 \_ 回拨   |
| 例程需要操作的最终状态。                                                                                                                               | 通过进行操作，需要微筛选器来调用 postoperation 回调例程。                                                     | FLT \_ PREOP \_ SUCCESS \_ \_ |
| 微筛选器必须完成或在以后继续处理此操作。                                                                                                     | 将操作置于挂起状态。 请稍后使用 [**FltCompletePendedPreOperation**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcompletependedpreoperation) 完成此操作。 请注意，返回 **FLT_PREOP_PENDING** 的预操作例程与调用 **FltCompletePendingOperation** 之间可能存在可接受的争用。 筛选器管理器将处理此方案，而无需从驱动程序输入。 | FLT \_ PREOP \_ 挂起                 |
| Postoperation 处理必须在调用调度例程的线程的上下文中发生。 这可确保一致的 IRQL 并维护本地变量状态。 | 将操作与 postoperation 同步。                                                                                                    | FLT \_ PREOP \_ 同步             |
| Preoperation 回调例程需要完成此操作。                                                                                                                    | 停止处理操作并分配最终的 NTSTATUS 值。                                                                                   | FLT \_ PREOP \_ 完成                |


每个 preoperation 回调例程定义如下：

```cpp
typedef FLT_PREOP_CALLBACK_STATUS 
(*PFLT_PRE_OPERATION_CALLBACK) ( 
    IN OUT PFLT_CALLBACK_DATA Data, 
    IN PCFLT_RELATED_OBJECTS FltObjects, 
    OUT PVOID *CompletionContext 
    ); 
```

与调度例程一样，preoperation 回调例程可以在 IRQL = 被动 \_ 级别或在 irql = APC \_ 级别调用。 通常，它在 \_ 发起 i/o 请求的线程的上下文中以 IRQL = 被动级别进行调用。 对于快速 i/o 和文件系统筛选器 (FsFilter) 操作，preoperation 回调例程始终以 IRQL = 被动 \_ 级别调用。 但是，对于基于 IRP 的操作，如果较高的筛选器或微微筛选器驱动程序 pends 操作以供工作线程处理，则可以在系统工作线程的上下文中调用微筛选器驱动程序的 preoperation 回调例程。

无法在 IRQL APC 级别的 postoperation 例程中检索上下文对象 &gt; \_ 。 相反，请在 preoperation 例程期间获取上下文对象并将其传递给 postoperation 例程，或在 IRQL &lt; = APC 级别执行 postoperation 处理 \_ 。 有关上下文的详细信息，请参阅 [管理上下文](managing-contexts.md)。

当筛选器管理器为给定 i/o 操作调用微筛选器驱动程序的 preoperation 回调例程时，微筛选器驱动程序会暂时控制 i/o 操作。 微筛选器驱动程序会保留此控件，直到它执行以下操作之一：

-   \_从 preoperation 回调例程返回 FLT PREOP 以外的状态值 \_ 。

-   从处理在 preoperation 回调例程中挂起的操作的工作例程调用 [**FltCompletePendedPreOperation**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcompletependedpreoperation) 。

本节包括：

[将 i/o 操作向下传递微筛选器实例堆栈](passing-an-i-o-operation-down-the-minifilter-driver-instance-stack.md)

[在 Preoperation 回调例程中完成 i/o 操作](completing-an-i-o-operation-in-a-preoperation-callback-routine.md)

[禁止在 Preoperation 回调例程中使用快速 i/o 操作](disallowing-a-fast-i-o-operation-in-a-preoperation-callback-routine.md)

[挂起 Preoperation 回调例程中的 i/o 操作](pending-an-i-o-operation-in-a-preoperation-callback-routine.md)

 

