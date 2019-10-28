---
title: 如何执行完成处理
description: 如何执行完成处理
ms.assetid: 5741c226-9781-4d9a-b6dd-d8ecc17c4c6f
keywords:
- IRP 完成例程 WDK 文件系统，处理阶段
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fcc3d6956d5ea16df7e7bd38dbcf9b8aa19134c9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841221"
---
# <a name="how-completion-processing-is-performed"></a>如何执行完成处理


## <span id="ddk_how_completion_processing_is_performed_if"></span><span id="DDK_HOW_COMPLETION_PROCESSING_IS_PERFORMED_IF"></span>


完成处理分两个阶段执行。 第一个阶段是在任意线程上下文中执行的，以 IRQL &lt;= 调度\_级别。 在此阶段中，将执行以下任务：

-   为 IRP 注册的每个完成例程将依次调用，从最低 IRP 堆栈位置开始。 如果完成例程返回状态\_\_需要更多的\_处理，则将停止完成处理。

-   如果 IRP 包含内存描述符列表（MDL），则由 MDL 映射的所有物理页面都将解除锁定。

-   I/o 完成的第二个阶段作为特殊内核 APC 排队给目标（请求）线程。

第二个阶段是在发起 i/o 请求的线程的上下文中执行的。 它作为特殊内核 APC 执行，因此在每个\_级别的 IRQL 运行。 在此阶段中，将执行以下任务：

-   如果 IRP 表示缓冲的操作，则会将**irp&gt;** 的内容复制&gt;到 SystemBuffer **UserBuffer**。

-   如果 IRP 包含 MDL，则会释放 MDL。

-   **Irp&gt;IoStatus**的内容将复制到**irp&gt;UserIosb** ，以便 i/o 请求的发起方可以查看操作的最终状态。

-   如果已在**Irp&gt;UserEvent**中提供事件，则会发出信号。 否则，如果此 IRP 有一个 file 对象，则会向其发出事件信号。

-   如果 IRP 是通过调用[**IoBuildDeviceIoControlRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuilddeviceiocontrolrequest)或[**IoBuildSynchronousFsdRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuildsynchronousfsdrequest)创建的，则它会从线程的挂起 i/o 请求列表中取消排队。

-   如果调用方请求了一个用户，则会将该用户排入队列。

-   IRP 已释放。

**请注意**   如果已停止 IRP 的完成处理，因为完成例程返回状态\_更多\_处理\_需要，可以通过在同一 IRP 上调用[**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)来恢复。 发生这种情况时，第一步处理会恢复，从紧靠其完成例程返回状态的驱动程序的完成例程开始，\_\_需要更多的\_处理。

 

 

 




