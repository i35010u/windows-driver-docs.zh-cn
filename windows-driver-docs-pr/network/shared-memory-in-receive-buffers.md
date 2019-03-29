---
title: 接收缓冲区中的共享内存
description: 接收缓冲区中的共享内存
ms.assetid: 3e4d0534-3cbd-40df-b7c1-4f2c15bcd757
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8c89f14edf1f48f555134913bf7c6118833e51fe
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575408"
---
# <a name="shared-memory-in-receive-buffers"></a>接收缓冲区中的共享内存





本部分中描述的布局的共享内存中 VMQ 接收缓冲区。接收指示有关使用中的缓冲区的详细信息，请参阅[VMQ 接收路径](vmq-receive-path.md)。

如果基础协议驱动程序设置 NDIS\_接收\_队列\_参数\_预测先行\_拆分\_中的必需标志**标志**的成员[ **NDIS\_接收\_队列\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff567211)结构，网络适配器应拆分某偏移量处接收的数据包等于或大于请求的预期大小和使用 DMA 将预测先行数据和预测先行开机自检数据传输到单独的共享的内存段。

微型端口驱动程序指定预期类型的设置 (**NdisSharedMemoryUsageReceiveLookahead**) 或其他共享的内存类型分配的共享的内存时。 例如，微型端口驱动程序调用[ **NdisAllocateSharedMemory** ](https://msdn.microsoft.com/library/windows/hardware/ff561616)函数和集**使用情况**中的成员[ **NDIS\_共享\_内存\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff567303)结构**NdisSharedMemoryUsageReceiveLookahead**。 队列分配完成后，微型端口驱动程序应为队列分配共享的内存。 有关分配和释放队列的共享的内存资源的信息，请参阅[共享的内存资源分配](shared-memory-resource-allocation.md)。

下图显示的网络数据的关系时传入数据拆分为两个共享的内存缓冲区。

![当传入数据拆分为两个共享的内存缓冲区时说明网络数据的关系的关系图](images/vmqpacket.png)

[ **NET\_缓冲区\_共享\_内存**](https://msdn.microsoft.com/library/windows/hardware/ff568419)结构指定共享的内存的信息。 可以有此类与关联的共享的内存缓冲区的链接的列表[ **NET\_缓冲区**](https://msdn.microsoft.com/library/windows/hardware/ff568376)结构。

使用[ **NET\_缓冲区\_共享\_内存优化\_下一步\_段**](https://msdn.microsoft.com/library/windows/hardware/ff568726)， [ **NET\_缓冲区\_共享\_内存优化\_标志**](https://msdn.microsoft.com/library/windows/hardware/ff568420)， [ **NET\_缓冲区\_共享\_内存优化\_处理**](https://msdn.microsoft.com/library/windows/hardware/ff568421)， [ **NET\_缓冲区\_共享\_内存优化\_偏移量**](https://msdn.microsoft.com/library/windows/hardware/ff568727)，和[**NET\_缓冲区\_共享\_内存优化\_长度**](https://msdn.microsoft.com/library/windows/hardware/ff568725)宏，以访问 NET\_缓冲区\_共享\_内存中 NET\_缓冲区结构。 **SharedMemoryInfo** NET 成员\_缓冲区结构包含第一个 NET\_缓冲区\_共享\_链接列表中的内存结构。

**请注意**  从 NDIS 6.30 开始，将数据包数据拆分为单独的预测先行缓冲区不再受支持。 从 Windows Server 2012 开始，基础协议驱动程序不会设置**NDIS\_接收\_队列\_参数\_预测先行\_拆分\_必需**中的标志**标志**的成员[ **NDIS\_接收\_队列\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff567211)结构。

 

 

 





