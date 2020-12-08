---
title: 在后操作回调例程中让 I/O 操作失败
description: 在后操作回调例程中让 I/O 操作失败
keywords:
- postoperation 回调例程 WDK 文件系统微筛选器，失败的操作
- 失败 i/o 操作 WDK 文件系统微筛选器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3af9f7567e953ccf8122a17660c0f03c8e0f8bd2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96826533"
---
# <a name="failing-an-io-operation-in-a-postoperation-callback-routine"></a>在后操作回调例程中让 I/O 操作失败


## <span id="ddk_failing_an_io_operation_in_a_postoperation_callback_routine_if"></span><span id="DDK_FAILING_AN_IO_OPERATION_IN_A_POSTOPERATION_CALLBACK_ROUTINE_IF"></span>


微筛选器驱动程序的 [**postoperation 回调例程**](/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_post_operation_callback) 可能会使 i/o 操作失败，但只是失败了 i/o 操作不会撤消操作的效果。 微筛选器驱动程序负责执行撤消操作所需的任何处理。

例如，微筛选器驱动程序的创建后回调例程可能会 \_ \_ 通过执行以下步骤使 IRP MJ 创建操作失败：

1.  调用 [**FltCancelFileOpen**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcancelfileopen) 关闭创建操作创建或打开的文件。 请注意， **FltCancelFileOpen** 不会撤消对该文件所做的任何修改。 例如， **FltCancelFileOpen** 不删除新创建的文件或将截断的文件还原到其以前的大小。

2.  将回调数据结构的 **IoStatus** 字段设置为该操作的最终 NTSTATUS 值。 此值必须是有效的错误 NTSTATUS 值，如 " \_ 拒绝访问" 状态 \_ 。

3.  将回调数据结构的 **IoStatus** 字段设置为零。

4.  返回 FLT \_ POSTOP \_ 已完成 \_ 处理。

将回调数据结构的 **IoStatus** 字段设置为操作的最终 NTSTATUS 值时，微筛选器驱动程序必须指定有效的错误 NTSTATUS 值。 请注意，微筛选器驱动程序无法指定 STATUS \_ FLT 不 \_ 允许 \_ 快速 \_ IO; 只有筛选器管理器才能使用此 NTSTATUS 值。

[**FltCancelFileOpen**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcancelfileopen)的调用方必须以 IRQL &lt; = APC \_ 级别运行。 但是，微筛选器驱动程序可以从创建后的回调例程安全调用此例程，因为对于 IRP \_ MJ \_ 创建操作， \_ 在发起创建操作的线程的上下文中，将在 IRQL = 被动级别调用 postoperation 回调例程。

 

