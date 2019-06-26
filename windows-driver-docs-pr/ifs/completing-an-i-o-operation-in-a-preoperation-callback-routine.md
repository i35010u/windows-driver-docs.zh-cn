---
title: 在预操作回调例程中完成 I/O 操作
description: 在预操作回调例程中完成 I/O 操作
ms.assetid: 1f339779-dc88-4673-87d5-36cee0b27fc2
keywords:
- preoperation 回调例程 WDK 文件系统微筛选器，完成 I/O 操作
- 完成 I/O 请求 WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 75e86633734557212d3429dc5a784bf2bdb9c58a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378981"
---
# <a name="completing-an-io-operation-in-a-preoperation-callback-routine"></a>在预操作回调例程中完成 I/O 操作


## <span id="ddk_completing_an_io_operation_in_a_preoperation_callback_routine_if"></span><span id="DDK_COMPLETING_AN_IO_OPERATION_IN_A_PREOPERATION_CALLBACK_ROUTINE_IF"></span>


向*完整*I/O 操作意味着暂停处理操作，将其分配一个最终的 NTSTATUS 值，并将其返回到筛选器管理器。

微筛选器驱动程序完成某个 I/O 操作，筛选器管理器执行以下任务：

-   下面当前微筛选器驱动程序的微筛选器驱动程序、 旧筛选器，或文件系统，则不发送该操作。

-   调用[ **postoperation 回调例程**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nc-fltkernel-pflt_post_operation_callback)上面微筛选器驱动程序实例堆栈中的当前微筛选器驱动程序的微筛选器驱动程序。

-   如果存在，不会为该操作，调用当前微筛选器驱动程序的 postoperation 回调例程。

微筛选器驱动程序[ **preoperation 回调例程**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nc-fltkernel-pflt_pre_operation_callback)完成某个 I/O 操作，请执行以下步骤：

1.  设置的回调数据结构**IoStatus.Status**字段为该操作的最终 NTSTATUS 值。

2.  返回 FLT\_PREOP\_完成。

完成某个 I/O 操作的 preoperation 回调例程不能设置非 NULL 完成上下文 (在*CompletionContext*输出参数)。

微筛选器驱动程序还可以完成的工作例程中的操作之前挂起 I/O 操作，请执行以下步骤：

1.  设置的回调数据结构**IoStatus.Status**字段为该操作的最终 NTSTATUS 值。

2.  传递 FLT\_PREOP\_中完成*CallbackStatus*参数时的工作例程调用[ **FltCompletePendedPreOperation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltcompletependedpreoperation)。

微筛选器驱动程序在完成某个 I/O 操作，必须设置的回调数据结构**IoStatus.Status**到该操作的最终 NTSTATUS 值，但此 NTSTATUS 值的字段不能为状态\_PENDING 或状态\_FLT\_禁止\_快速\_IO。 对于清除或关闭操作，此字段必须是状态\_成功。 不能与任何其他 NTSTATUS 值完成这些操作。

完成某个 I/O 操作通常称为上成功或失败的操作，具体取决于 NTSTATUS 值：

-   向*成功*I/O 操作意味着若要完成与成功或信息性 NTSTATUS 值，如状态\_成功。

-   向*失败*I/O 操作意味着若要完成使用错误或警告 NTSTATUS 值，如状态\_无效\_设备\_请求或状态\_缓冲区\_溢出。

NTSTATUS 值 ntstatus.h 中发现了定义。 这些值划分为四个类别： 成功后，信息性消息、 警告和错误。 有关这些值的详细信息，请参阅[使用 NTSTATUS 值](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-ntstatus-values)。

 

 




