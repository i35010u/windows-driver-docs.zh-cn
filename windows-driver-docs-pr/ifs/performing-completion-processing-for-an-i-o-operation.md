---
title: 执行 I/O 操作的完成处理
description: 执行 I/O 操作的完成处理
ms.assetid: 7e65c21c-d38f-4804-8c07-6cd89f6a6dd6
keywords:
- postoperation 回调例程 WDK 文件系统微筛选器，完成处理
- 完成 i/o 请求 WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4e606880851e458e9ced10497ed7078aa7975822
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89063278"
---
# <a name="performing-completion-processing-for-an-io-operation"></a>执行 I/O 操作的完成处理


## <span id="ddk_performing_completion_processing_for_an_io_operation_if"></span><span id="DDK_PERFORMING_COMPLETION_PROCESSING_FOR_AN_IO_OPERATION_IF"></span>


当基础文件系统、旧筛选器或位于微筛选器驱动程序实例堆栈中较低级别的其他微筛选器驱动程序完成 i/o 操作时，将调用微筛选器驱动程序的 [**postoperation 回调例程**](/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_post_operation_callback) 。

此外，当筛选器驱动程序实例被破坏时，筛选器管理器会 "耗尽" 实例已收到 [**preoperation 回调**](/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_pre_operation_callback) 并等待 [**postoperation 回调**](/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_post_operation_callback)的任何 i/o 操作。 在这种情况下，筛选器管理器将调用微筛选器驱动程序的 postoperation 回调例程，即使 i/o 操作尚未完成，还会 \_ \_ \_ 在 *Flags* 输入参数中设置 FLTFL POST 操作排出标志。

\_设置 FLTFL POST \_ 操作 \_ 排出标志后，微筛选器驱动程序不得执行正常的完成处理。 相反，它仅应执行必要的清理操作，例如释放微筛选器驱动程序为其 preoperation 回调例程中的 *CompletionContext* 参数分配的内存，并返回 FLT \_ POSTOP \_ 完成的 \_ 处理。

本部分包括以下主题：

[确保在安全的 IRQL 处执行完成处理](ensuring-that-completion-processing-is-performed-at-safe-irql.md)

 

