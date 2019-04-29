---
title: 如何执行完成处理
description: 如何执行完成处理
ms.assetid: 5741c226-9781-4d9a-b6dd-d8ecc17c4c6f
keywords:
- IRP 完成例程 WDK 文件系统，处理阶段
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6016144ede00ebe471928c0bacd3681d82350d6b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63370129"
---
# <a name="how-completion-processing-is-performed"></a>如何执行完成处理


## <span id="ddk_how_completion_processing_is_performed_if"></span><span id="DDK_HOW_COMPLETION_PROCESSING_IS_PERFORMED_IF"></span>


在两个阶段中执行完成处理。 第一阶段执行在任意线程上下文中，在 IRQL &lt;= 调度\_级别。 在此阶段中，执行以下任务：

-   从最低 IRP 堆栈位置开始依次调用为 IRP 注册每个完成例程。 如果完成例程返回状态\_更多\_处理\_必需的完成处理将暂停。

-   如果 IRP 包含内存描述符列表 (MDL)，由 MDL 映射任何物理页面会被锁定。

-   I/O 完成的第二个阶段列入作为特殊内核 APC 的 （请求） 的目标线程。

第二个阶段是在发起 I/O 请求的线程上下文中执行的。 它作为特殊内核 APC 执行，因此，运行在 IRQL APC\_级别。 在此阶段中，执行以下任务：

-   如果 IRP 表示缓冲的操作的内容**Irp-&gt;AssociatedIrp.SystemBuffer**复制到**Irp-&gt;UserBuffer**。

-   如果 IRP 包含 MDL，会释放 MDL。

-   内容**Irp-&gt;IoStatus**复制到**Irp-&gt;UserIosb**以便 I/O 请求的发起方可以看到该操作的最终状态。

-   如果事件中提供**Irp-&gt;UserEvent**，它发出信号。 否则，如果没有此 IRP 的文件对象，其事件发出信号。

-   如果通过调用创建 IRP [ **IoBuildDeviceIoControlRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff548318)或[ **IoBuildSynchronousFsdRequest**](https://msdn.microsoft.com/library/windows/hardware/ff548330)，从取消排队线程的挂起 I/O 请求列表。

-   如果调用方请求一个，APC 的用户将会排队。

-   IRP，将释放。

**请注意**  由于完成例程返回状态，因此，如果停止完成处理 IRP\_详细\_处理\_必需的它可以恢复通过调用[ **IoCompleteRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff548343)上相同的 IRP。 在此情况下，第一阶段处理将继续，从上一个紧邻的驱动程序完成例程其完成例程返回状态\_更多\_处理\_必需。

 

 

 




