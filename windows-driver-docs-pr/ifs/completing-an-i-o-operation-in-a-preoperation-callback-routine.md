---
title: 在预操作回调例程中完成 I/O 操作
description: 在预操作回调例程中完成 I/O 操作
keywords:
- preoperation 回调例程 WDK 文件系统微筛选器，完成 i/o 操作
- 完成 i/o 请求 WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8709986a556fd6202b5aac136c28f91cc9c50158
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838789"
---
# <a name="completing-an-io-operation-in-a-preoperation-callback-routine"></a>在预操作回调例程中完成 I/O 操作


## <span id="ddk_completing_an_io_operation_in_a_preoperation_callback_routine_if"></span><span id="DDK_COMPLETING_AN_IO_OPERATION_IN_A_PREOPERATION_CALLBACK_ROUTINE_IF"></span>


若要 *完成* i/o 操作，请为该操作暂停处理，为其分配一个最终的 NTSTATUS 值，并将其返回到筛选器管理器。

当微筛选器驱动程序完成 i/o 操作时，筛选器管理器将执行以下操作：

-   不会将操作发送到当前微筛选器驱动程序下的微筛选器驱动程序、旧筛选器或文件系统。

-   在微筛选器驱动程序实例堆栈中的当前微微筛选器驱动程序之前调用微筛选器驱动程序的 [**postoperation 回调例程**](/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_post_operation_callback) 。

-   不会为操作（如果有）调用当前微筛选器驱动程序的 postoperation 回调例程。

微筛选器驱动程序的 [**preoperation 回调例程**](/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_pre_operation_callback) 通过执行以下步骤完成 i/o 操作：

1.  将回调数据结构的 **IoStatus** 字段设置为该操作的最终 NTSTATUS 值。

2.  返回 FLT \_ PREOP \_ 完成。

完成 i/o 操作的 preoperation 回调例程无法在 *CompletionContext* output 参数) 中 (设置非 NULL 完成上下文。

微筛选器驱动程序还可以通过执行以下步骤，在工作例程中完成先前挂起的 i/o 操作的操作：

1.  将回调数据结构的 **IoStatus** 字段设置为该操作的最终 NTSTATUS 值。

2.  \_ \_ 当工作例程调用 [**FltCompletePendedPreOperation**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcompletependedpreoperation)时，传递 FLT PREOP 在 *CallbackStatus* 参数中完成。

完成 i/o 操作时，微筛选器驱动程序必须将回调数据结构的 **IoStatus** 字段设置为该操作的最终 NTSTATUS 值，但此 NTSTATUS 值不能为状态 "挂起" \_ 或 "状态 \_ FLT 不 \_ 允许 \_ 快速 IO" \_ 。 对于清理或关闭操作，该字段的状态必须为 " \_ 成功"。 不能用任何其他 NTSTATUS 值来完成这些操作。

完成 i/o 操作通常被称为 "成功" 或 "失败" 操作，具体取决于 NTSTATUS 值：

-   若要 *成功* 执行 i/o 操作，请使用成功或信息性的 NTSTATUS 值（如状态成功）完成此操作 \_ 。

-   若要使 i/o 操作 *失败* ，请使用错误或警告 NTSTATUS 值来完成此操作，如状态 \_ 无效的 \_ 设备 \_ 请求或状态 \_ 缓冲区 \_ 溢出。

NTSTATUS 值在 ntstatus 中定义。 这些值分为四类：成功、信息性、警告和错误。 有关这些值的详细信息，请参阅 [使用 NTSTATUS 值](../kernel/using-ntstatus-values.md)。

 

