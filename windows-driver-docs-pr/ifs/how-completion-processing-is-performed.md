---
title: 如何执行完成处理
description: 如何执行完成处理
ms.assetid: 5741c226-9781-4d9a-b6dd-d8ecc17c4c6f
keywords:
- IRP 完成例程 WDK 文件系统，处理阶段
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: eac2526a3f9047f64c5e2157ecd7cd373a12a93f
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89063342"
---
# <a name="how-completion-processing-is-performed"></a>如何执行完成处理


## <span id="ddk_how_completion_processing_is_performed_if"></span><span id="DDK_HOW_COMPLETION_PROCESSING_IS_PERFORMED_IF"></span>


完成处理分两个阶段执行。 第一阶段在任意线程上下文中执行，以 IRQL &lt; = 调度 \_ 级别。 在此阶段中，将执行以下任务：

-   为 IRP 注册的每个完成例程将依次调用，从最低 IRP 堆栈位置开始。 如果完成例程返回状态 \_ \_ "需要更多 \_ 的处理"，则将停止完成处理。

-   如果 IRP 包含 (MDL) 的内存描述符列表，则由 MDL 映射的所有物理页面都将解除锁定。

-   I/o 完成的第二个阶段将排队等候目标 (请求) 线程作为特殊内核 APC。

第二个阶段是在发起 i/o 请求的线程的上下文中执行的。 它作为特殊内核 APC 执行，因此在 IRQL \_ 级别运行。 在此阶段中，将执行以下任务：

-   如果 IRP 表示缓冲操作，则会将 **irp &gt;AssociatedIrp.SystemBuffer** 的内容复制到 ** &gt; UserBuffer**。

-   如果 IRP 包含 MDL，则会释放 MDL。

-   将 ** &gt; IoStatus** 的内容复制到 ** &gt; UserIosb** ，以便 i/o 请求的发起方可以查看操作的最终状态。

-   如果已在 **Irp- &gt; UserEvent**中提供事件，则会发出信号。 否则，如果此 IRP 有一个 file 对象，则会向其发出事件信号。

-   如果 IRP 是通过调用 [**IoBuildDeviceIoControlRequest**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuilddeviceiocontrolrequest) 或 [**IoBuildSynchronousFsdRequest**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuildsynchronousfsdrequest)创建的，则它会从线程的挂起 i/o 请求列表中取消排队。

-   如果调用方请求了一个用户，则会将该用户排入队列。

-   IRP 已释放。

**注意**   如果已停止 IRP 的完成处理，因为完成例程返回状态 \_ \_ "需要更多 \_ 的处理"，则可以通过在同一 IRP 上调用[**IoCompleteRequest**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)来恢复该完成。 当发生这种情况时，将继续执行第一步处理，从驱动程序的完成例程开始，其完成例程返回状态 " \_ 需要更多 \_ 处理" \_ 。

 

 

