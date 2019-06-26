---
title: 在后操作回调例程中让 I/O 操作失败
description: 在后操作回调例程中让 I/O 操作失败
ms.assetid: 45897bca-1573-42c5-ad00-3198b7362d9e
keywords:
- postoperation 回调例程 WDK 文件系统微筛选器，失败的操作
- 失败的 I/O 操作 WDK 文件系统微筛选器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 78c92a854add62ef67d3567c52f736b90ef43d87
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386085"
---
# <a name="failing-an-io-operation-in-a-postoperation-callback-routine"></a>在后操作回调例程中让 I/O 操作失败


## <span id="ddk_failing_an_io_operation_in_a_postoperation_callback_routine_if"></span><span id="DDK_FAILING_AN_IO_OPERATION_IN_A_POSTOPERATION_CALLBACK_ROUTINE_IF"></span>


微筛选器驱动程序[ **postoperation 回调例程**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nc-fltkernel-pflt_post_operation_callback)可能会失败的 I/O 操作成功，但只失败的 I/O 操作不会撤消该操作的效果。 微筛选器驱动程序负责执行撤消操作所需的任何处理。

例如，微筛选器驱动程序后创建回调例程可能会失败成功 IRP\_MJ\_通过执行以下步骤创建操作：

1.  调用[ **FltCancelFileOpen** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltcancelfileopen)关闭此文件已创建或打开的创建操作。 请注意， **FltCancelFileOpen**不会撤消对文件进行任何修改。 例如， **FltCancelFileOpen**不会删除新创建的文件或截断的文件还原到其以前的大小。

2.  设置的回调数据结构**IoStatus.Status**字段为该操作的最终 NTSTATUS 值。 此值必须是有效的错误 NTSTATUS 值，如状态\_访问\_被拒绝。

3.  设置的回调数据结构**IoStatus.Information**字段为零。

4.  返回 FLT\_POSTOP\_已完成\_处理。

设置的回调数据结构时**IoStatus.Status**字段为该操作，微筛选器驱动程序的最终 NTSTATUS 值必须指定有效的错误 NTSTATUS 值。 请注意，微筛选器驱动程序不能指定状态\_FLT\_禁止\_快速\_IO; 只有筛选器管理器可以使用此 NTSTATUS 值。

调用方[ **FltCancelFileOpen** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltcancelfileopen)必须在 IRQL 运行&lt;= APC\_级别。 但是，微筛选器驱动程序可以安全地调用此例程后创建回调例程，因为，对于 IRP\_MJ\_创建操作在 IRQL 调用 postoperation 回调例程 = 被动\_级别，请在发起创建操作的线程上下文。

 

 




