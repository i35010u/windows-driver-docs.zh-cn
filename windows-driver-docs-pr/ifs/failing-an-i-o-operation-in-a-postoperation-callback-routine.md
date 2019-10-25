---
title: 在后操作回调例程中让 I/O 操作失败
description: 在后操作回调例程中让 I/O 操作失败
ms.assetid: 45897bca-1573-42c5-ad00-3198b7362d9e
keywords:
- postoperation 回调例程 WDK 文件系统微筛选器，失败的操作
- 失败 i/o 操作 WDK 文件系统微筛选器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5e6c04094ddb327357b77d8dd5918e17afa621d8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841419"
---
# <a name="failing-an-io-operation-in-a-postoperation-callback-routine"></a>在后操作回调例程中让 I/O 操作失败


## <span id="ddk_failing_an_io_operation_in_a_postoperation_callback_routine_if"></span><span id="DDK_FAILING_AN_IO_OPERATION_IN_A_POSTOPERATION_CALLBACK_ROUTINE_IF"></span>


微筛选器驱动程序的[**postoperation 回调例程**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_post_operation_callback)可能会使 i/o 操作失败，但只是失败了 i/o 操作不会撤消操作的效果。 微筛选器驱动程序负责执行撤消操作所需的任何处理。

例如，微筛选器驱动程序的创建后回调例程可能会通过执行以下步骤，使成功的 IRP\_MJ\_创建操作失败：

1.  调用[**FltCancelFileOpen**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcancelfileopen)关闭创建操作创建或打开的文件。 请注意， **FltCancelFileOpen**不会撤消对该文件所做的任何修改。 例如， **FltCancelFileOpen**不删除新创建的文件或将截断的文件还原到其以前的大小。

2.  将回调数据结构的**IoStatus**字段设置为该操作的最终 NTSTATUS 值。 此值必须是有效的错误 NTSTATUS 值，如\_访问\_拒绝的状态。

3.  将回调数据结构的**IoStatus**字段设置为零。

4.  返回 FLT\_POSTOP\_完成\_处理。

将回调数据结构的**IoStatus**字段设置为操作的最终 NTSTATUS 值时，微筛选器驱动程序必须指定有效的错误 NTSTATUS 值。 请注意，微筛选器驱动程序不能\_FLT 指定状态\_不允许\_快速\_IO;只有筛选器管理器可以使用此 NTSTATUS 值。

[**FltCancelFileOpen**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcancelfileopen)的调用方必须以 IRQL &lt;= APC\_级别运行。 但是，微筛选器驱动程序可以通过创建后回调例程安全地调用此例程，因为对于 IRP\_MJ\_创建操作，在线程的上下文中，在 IRQL = 被动\_级别调用 postoperation 回调例程这是因为创建操作。

 

 




