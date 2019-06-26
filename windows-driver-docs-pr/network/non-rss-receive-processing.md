---
title: 非 RSS 接收处理
description: 非 RSS 接收处理
ms.assetid: 9fe262c3-9ce5-4625-8d29-ff7dc4ccb90a
keywords:
- 接收方缩放 WDK 网络，非 RSS 接收处理
- RSS 网络 WDK，非 RSS 接收处理
- 非 RSS 接收处理 WDK RSS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 03f0397ab37d1be760e76b5e1b348777d36142d9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371207"
---
# <a name="non-rss-receive-processing"></a>非 RSS 接收处理





本主题中所述，不支持 RSS 的句柄的微型端口驱动程序将接收处理。

下图说明了非 RSS 接收处理。

![关系图说明如何发送和接收处理，未 rss](images/rsslessstack.png)

在图中，虚线的路径表示备用路径用于发送和接收处理。 由于系统控制的缩放，因此不会始终在提供最佳性能的 CPU 上进行处理。 连接同一 CPU 上通过连续中断仅由处理机会。

为每个非 RSS 中断周期重复以下过程：

1.  NIC 使用 DMA 与接收的数据填充缓冲区并中断系统。

    微型端口驱动程序在初始化期间分配共享内存中的接收缓冲区。

2.  NIC 可以继续阅读其他填充此中断周期中随时接收缓冲区。 但是，NIC 不会中断再次直到微型端口驱动程序启用中断。

    系统在一个中断周期中处理的接收的缓冲区可以与多个不同的网络连接相关联。

3.  NDIS 调用微型端口驱动程序[ *MiniportInterrupt* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_isr)系统确定 CPU 上的函数 (ISR)。

    理想情况下，ISR 应转到最不忙的 CPU。 但是，在某些系统中，系统会分配 ISR 到可用的 CPU 或与 NIC 关联的 CPU

4.  ISR 禁用中断和请求 NDIS 排队延迟的过程调用 (DPC) 来处理接收到的数据。

5.  NDIS 调用[ *MiniportInterruptDPC* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_interrupt_dpc)函数 (DPC) 上当前的 CPU。

6.  DPC 生成接收所有的接收缓冲区描述符，并指示驱动程序堆栈上的数据。 有关详细信息，请参阅[接收网络数据](receiving-network-data.md)。

    可以有多的缓冲区的许多不同的连接并且可能没有执行大量的处理才能完成。 在上其他 Cpu 处理接收到的数据与后续中断周期相关联。 处理给定的网络连接的发送也可以不同 CPU 上运行。

7.  DPC 启用中断。 此中断周期已完成，此过程再次启动。

 

 





