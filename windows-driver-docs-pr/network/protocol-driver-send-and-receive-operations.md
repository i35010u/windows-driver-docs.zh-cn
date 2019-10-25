---
title: 协议驱动程序发送和接收操作
description: 协议驱动程序发送和接收操作
ms.assetid: c621d673-167e-41e1-a121-68e0d0bc6f8a
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c8b8ca1752ad284f47cf3bffd625eefe26211398
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844908"
---
# <a name="protocol-driver-send-and-receive-operations"></a>协议驱动程序发送和接收操作





协议驱动程序发出发送请求并处理底层驱动程序的接收指示。 在单个函数调用中，NDIS 协议驱动程序可以将多个 net [ **\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构发送到每个 NET\_缓冲区\_列表结构的多个 NET [ **\_缓冲**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)结构。 在接收路径中，协议驱动程序可以接收 NET\_缓冲区\_列表结构的列表。

协议驱动程序必须管理发送缓冲池。 正确管理此类池需要预先分配足够的缓冲区空间来优化系统性能。

以下主题提供了有关协议驱动程序缓冲区管理、发送操作和接收操作的详细信息：

[协议驱动程序缓冲区管理](protocol-driver-buffer-management.md)

[从协议驱动程序发送数据](sending-data-from-a-protocol-driver.md)

[接收协议驱动程序中的数据](receiving-data-in-protocol-drivers.md)

 

 





