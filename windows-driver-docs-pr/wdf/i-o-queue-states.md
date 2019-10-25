---
title: I/O 队列状态
description: I/O 队列状态
ms.assetid: 99519d1c-20e5-4a32-8462-19ec9f907506
keywords:
- I/o 队列 WDK KMDF，状态
- 状态 WDK i/o 队列
- 当前 i/o 队列状态 WDK KMDF
- 空闲 i/o 队列状态 WDK KMDF
- 就绪 i/o 队列状态 WDK KMDF
- 已停止 i/o 队列状态 WDK KMDF
- 已排出 i/o 队列状态 WDK KMDF
- 已清除 i/o 队列状态 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0408d8aeaca95d4ad65b4ab7e1f8024a45e2c5db
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845212"
---
# <a name="io-queue-states"></a>I/O 队列状态


框架定义 i/o 队列的以下状态：

<a href="" id="idle"></a>*时间*  
I/o 队列不包含 i/o 请求，驱动程序未处理从 i/o 队列接收到的任何请求。

<a href="" id="ready"></a>*准备好*  
I/o 队列可从框架接收 i/o 请求，并可以将 i/o 请求传递给驱动程序。

<a href="" id="stopped"></a>*停下*  
I/o 队列可以从框架接收 i/o 请求，但不能将 i/o 请求传递给驱动程序，驱动程序也不会处理从 i/o 队列收到的任何请求。

<a href="" id="drained"></a>*排放*  
I/o 队列为空，它无法从框架接收到新的 i/o 请求，i/o 队列中的所有 i/o 请求都已传递给驱动程序。

<a href="" id="purged"></a>*清除*  
I/o 队列为空，它无法从框架接收到新的 i/o 请求，i/o 队列中的所有 i/o 请求都已被取消。

当驱动程序调用[**WdfIoQueueCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuecreate)后，框架可将新的 i/o 队列设置为就绪状态。 但是，仅当设备处于工作状态（D0）状态时，[电源托管 i/o 队列](using-power-managed-i-o-queues.md)才进入 "就绪" 状态。

驱动程序可以通过以下方式更改 i/o 队列的状态：

-   调用[**WdfIoQueueStop**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuestop)或[**WdfIoQueueStopSynchronously**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuestopsynchronously) ，使队列处于停止状态。

-   调用[**WdfIoQueueDrain**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuedrain)或[**WdfIoQueueDrainSynchronously**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuedrainsynchronously)将队列置于其排出状态。

-   调用[**WdfIoQueuePurge**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuepurge)或[**WdfIoQueuePurgeSynchronously**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuepurgesynchronously)以将队列置于其清除状态。

-   调用[**WdfIoQueueStart**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuestart)将队列返回到其就绪状态。

若要获取 i/o 队列的当前状态，驱动程序可以调用[**WdfIoQueueGetState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuegetstate)。

 

 





