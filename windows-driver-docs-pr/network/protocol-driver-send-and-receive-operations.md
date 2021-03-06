---
title: 协议驱动程序发送和接收操作
description: 协议驱动程序发送和接收操作
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 14620b7fb24f4b7de355c04e602d25d468fa01cb
ms.sourcegitcommit: a9fb2c30adf09ee24de8e68ac1bc6326ef3616b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2021
ms.locfileid: "102248147"
---
# <a name="protocol-driver-send-and-receive-operations"></a>协议驱动程序发送和接收操作





协议驱动程序发出发送请求并处理底层驱动程序的接收指示。 在单个函数调用中，NDIS 协议驱动程序可以在每个网络缓冲区列表结构上发送多个具有多个 [**网络 \_ 缓冲区**](/windows-hardware/drivers/ddi/nbl/ns-nbl-net_buffer)结构的 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/nbl/ns-nbl-net_buffer_list)结构 \_ \_ 。 在接收路径中，协议驱动程序可以接收网络 \_ 缓冲区 \_ 列表结构的列表。

协议驱动程序必须管理发送缓冲池。 正确管理此类池需要预先分配足够的缓冲区空间来优化系统性能。

以下主题提供了有关协议驱动程序缓冲区管理、发送操作和接收操作的详细信息：

[协议驱动程序缓冲区管理](protocol-driver-buffer-management.md)

[从协议驱动程序发送数据](sending-data-from-a-protocol-driver.md)

[在协议驱动程序中接收数据](receiving-data-in-protocol-drivers.md)

 

