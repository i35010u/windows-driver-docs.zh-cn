---
title: 协议驱动程序发送和接收操作
description: 协议驱动程序发送和接收操作
ms.assetid: c621d673-167e-41e1-a121-68e0d0bc6f8a
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 543cd0e1e96f693d3bcf9b3b16a5da28bf5fcc78
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385460"
---
# <a name="protocol-driver-send-and-receive-operations"></a>协议驱动程序发送和接收操作





协议驱动程序发起的发送请求和处理的基础驱动程序的接收指示。 在单个函数调用中，可以发送多个协议的 NDIS 驱动程序[ **NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)结构具有多个[ **NET\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer)每个网络上的结构\_缓冲区\_列表结构。 在接收路径中，协议驱动程序可以接收一系列 NET\_缓冲区\_列表结构。

协议驱动程序必须管理发送缓冲池。 适当管理这种池需要预先分配的缓冲区空间不足，为了优化系统性能。

以下主题提供有关协议驱动程序缓冲区管理的详细信息，发送操作，并接收操作：

[协议驱动程序缓冲区管理](protocol-driver-buffer-management.md)

[从协议驱动程序发送数据](sending-data-from-a-protocol-driver.md)

[协议驱动程序中接收数据](receiving-data-in-protocol-drivers.md)

 

 





