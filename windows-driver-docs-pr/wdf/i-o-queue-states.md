---
title: I/O 队列状态
description: I/O 队列状态
ms.assetid: 99519d1c-20e5-4a32-8462-19ec9f907506
keywords:
- I/O 队列 WDK KMDF，状态
- 指出 WDK I/O 队列
- 当前的 I/O 队列状态 WDK KMDF
- 空闲 I/O 队列状态 WDK KMDF
- 准备好的 I/O 队列状态 WDK KMDF
- 停止的 I/O 队列状态 WDK KMDF
- 排除 I/O 队列状态 WDK KMDF
- 清除 I/O 队列状态 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ec6ae9821b679d72821af5d10228bda4c8c530f9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382828"
---
# <a name="io-queue-states"></a>I/O 队列状态


框架定义的 I/O 队列的以下状态：

<a href="" id="idle"></a>*Idle*  
I/O 队列包含没有 I/O 请求，并且该驱动程序不处理它从 I/O 队列接收任何请求。

<a href="" id="ready"></a>*Ready*  
I/O 队列可以接收来自框架，I/O 请求，它可以将输入/输出请求传递到驱动程序。

<a href="" id="stopped"></a>*已停止*  
I/O 队列可以接收来自框架，I/O 请求，但它不能提供 I/O 请求的该驱动程序和驱动程序不处理它从 I/O 队列接收任何请求。

<a href="" id="drained"></a>*已耗尽*  
I/O 队列为空，它不能从框架，接收新的 I/O 请求和 I/O 队列中的所有 I/O 请求已都传递到驱动程序。

<a href="" id="purged"></a>*清除*  
I/O 队列为空，它不能从框架，接收新的 I/O 请求和 I/O 队列中的所有 I/O 请求都已被都取消。

驱动程序调用后，框架可以将新的 I/O 队列设置为就绪状态[ **WdfIoQueueCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nf-wdfio-wdfioqueuecreate)。 但是，[电源管理的 I/O 队列](using-power-managed-i-o-queues.md)进入就绪状态，仅当设备处于其工作 (D0) 状态。

您的驱动程序可以更改通过的 I/O 队列的状态：

-   调用[ **WdfIoQueueStop** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nf-wdfio-wdfioqueuestop)或[ **WdfIoQueueStopSynchronously** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nf-wdfio-wdfioqueuestopsynchronously)要将队列保存在其已停止状态。

-   调用[ **WdfIoQueueDrain** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nf-wdfio-wdfioqueuedrain)或[ **WdfIoQueueDrainSynchronously** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nf-wdfio-wdfioqueuedrainsynchronously)要将队列保存在其已用完状态。

-   调用[ **WdfIoQueuePurge** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nf-wdfio-wdfioqueuepurge)或[ **WdfIoQueuePurgeSynchronously** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nf-wdfio-wdfioqueuepurgesynchronously)要将队列保存在其已清除状态。

-   调用[ **WdfIoQueueStart** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nf-wdfio-wdfioqueuestart)返回为其准备就绪的状态队列。

若要获取的 I/O 队列的当前状态，您的驱动程序可以调用[ **WdfIoQueueGetState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nf-wdfio-wdfioqueuegetstate)。

 

 





