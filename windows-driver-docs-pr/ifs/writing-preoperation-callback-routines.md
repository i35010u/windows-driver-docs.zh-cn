---
title: 编写 Preoperation 回调例程
description: 编写 Preoperation 回调例程
ms.assetid: 3f863c44-152e-43c9-8ef5-ec426986a3fe
keywords:
- preoperation 回调例程 WDK 文件系统微筛选器、 编写
- 编写回调例程
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 06d29454c4f456bace594ecb11a55d83cc008731
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56545327"
---
# <a name="writing-preoperation-callback-routines"></a>编写 Preoperation 回调例程


## <span id="ddk_writing_preoperation_callback_routines_if"></span><span id="DDK_WRITING_PREOPERATION_CALLBACK_ROUTINES_IF"></span>


文件系统微筛选器驱动程序使用一个或多个*preoperation 回调例程*到筛选器 I/O 的操作。 [**Preoperation 回调例程**](https://msdn.microsoft.com/library/windows/hardware/ff551109)类似于传统的文件系统筛选器驱动程序中使用的调度例程。

微筛选器驱动程序通过将存储中的回调例程的入口点注册特定类型的 I/O 操作的 preoperation 回调例程**OperationRegistration**的成员[ **FLT\_注册**](https://msdn.microsoft.com/library/windows/hardware/ff544811)结构。 微筛选器驱动程序将此成员作为参数传递[ **FltRegisterFilter** ](https://msdn.microsoft.com/library/windows/hardware/ff544305)中其**DriverEntry**例程。

微筛选器驱动程序收到只有这些类型的 I/O 操作，它们具有为其注册 preoperation 或 postoperation 回调例程。 微筛选器驱动程序可以注册的情况下注册给定类型的 I/O 操作的 preoperation 回调例程[ **postoperation 回调例程**](https://msdn.microsoft.com/library/windows/hardware/ff551107)，反之亦然。

下表显示了一个特定的使用方案和它的返回值的 preoperation 回调例程实现。

| 使用方案                                                                                                                                                                        | 实现                                                                                                                                       | 返回值                      |
|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------|
| 例程不相关的操作和不需要操作的最终状态或具有不 postoperation 执行回调。                                             | 而不会在完成调用微筛选器的 postoperation 回调传递通过 I/O 操作。                                                | FLT\_PREOP\_成功\_否\_回调   |
| 例程需要操作的最终状态。                                                                                                                               | 将传递通过要求微筛选器来调用 postoperation 回调例程进行的操作。                                                     | FLT\_PREOP\_成功\_WITH\_回调 |
| 微筛选器必须完成或继续处理此操作在将来。                                                                                                     | 将置于挂起状态的操作。 使用[ **FltCompletePendedPreOperation** ](https://msdn.microsoft.com/library/windows/hardware/ff541913)完成此操作更高版本。 请注意，可能返回的预操作例程之间可接受争用**FLT_PREOP_PENDING**，并**FltCompletePendingOperation**被调用。 筛选器管理器处理这种情况下，而无需从驱动程序的输入。 | FLT\_PREOP\_PENDING                 |
| Postoperation 处理必须出现在同一线程的上下文中调用的调度例程。 这可确保一致的 IRQL 和维护您的本地变量状态。 | 与 postoperation 同步操作。                                                                                                    | FLT\_PREOP\_SYNCHRONIZE             |
| Preoperation 回调例程需要完成该操作。                                                                                                                    | 停止处理操作，并将分配 NTSTATUS 的最终值。                                                                                   | FLT\_PREOP\_完成                |


每个 preoperation 回调例程定义，如下所示：

```cpp
typedef FLT_PREOP_CALLBACK_STATUS 
(*PFLT_PRE_OPERATION_CALLBACK) ( 
    IN OUT PFLT_CALLBACK_DATA Data, 
    IN PCFLT_RELATED_OBJECTS FltObjects, 
    OUT PVOID *CompletionContext 
    ); 
```

可以像调度例程在 IRQL 中调用 preoperation 回调例程 = 被动\_层，或在 IRQL = APC\_级别。 通常称为在 IRQL = 被动\_级别，请在发起 I/O 请求的线程上下文中。 有关快速 I/O 和文件系统筛选器 (FsFilter) 操作，preoperation 调用回调例程始终在 IRQL = 被动\_级别。 但是，对于基于 IRP 的操作，微筛选器驱动程序的 preoperation 回调例程可以在上下文中调用的系统工作线程如果更高版本的筛选器或微筛选器驱动程序等待处理该操作由工作线程。

不能在 IRQL postoperation 例程中检索上下文对象&gt;APC\_级别。 相反，在 preoperation 例程期间获取的上下文对象，将其传递给 postoperation 例程或者执行 postoperation 处理在 IRQL &lt;= APC\_级别。 有关上下文的详细信息，请参阅[管理上下文](managing-contexts.md)。

当筛选器管理器调用指定的 I/O 操作时微筛选器驱动程序的 preoperation 回调例程时，微筛选器驱动程序将暂时控制 I/O 操作。 微筛选器驱动程序将保留此控件，直到它执行以下项之一：

-   返回的状态值不 FLT\_PREOP\_PENDING preoperation 回调例程。

-   调用[ **FltCompletePendedPreOperation** ](https://msdn.microsoft.com/library/windows/hardware/ff541913)从已处理被 preoperation 回调例程中的挂起的操作的工作例程。

本部分包括：

[传递微筛选器实例堆栈的下层的 I/O 操作](passing-an-i-o-operation-down-the-minifilter-driver-instance-stack.md)

[完成某个 I/O 操作中 Preoperation 回调例程](completing-an-i-o-operation-in-a-preoperation-callback-routine.md)

[不允许 Preoperation 回调例程中的快速 I/O 操作](disallowing-a-fast-i-o-operation-in-a-preoperation-callback-routine.md)

[挂起的 I/O 操作中 Preoperation 回调例程](pending-an-i-o-operation-in-a-preoperation-callback-routine.md)

 

 




