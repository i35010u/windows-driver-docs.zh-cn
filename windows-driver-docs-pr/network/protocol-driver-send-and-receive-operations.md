---
title: 协议驱动程序发送和接收操作
description: 协议驱动程序发送和接收操作
ms.assetid: c621d673-167e-41e1-a121-68e0d0bc6f8a
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a0e99979006246867dc2ff7d492c486d6e84ffa2
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89215140"
---
# <a name="protocol-driver-send-and-receive-operations"></a>协议驱动程序发送和接收操作





协议驱动程序发出发送请求并处理底层驱动程序的接收指示。 在单个函数调用中，NDIS 协议驱动程序可以在每个网络缓冲区列表结构上发送多个具有多个[**网络 \_ 缓冲区**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)结构的[**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构 \_ \_ 。 在接收路径中，协议驱动程序可以接收网络 \_ 缓冲区 \_ 列表结构的列表。

协议驱动程序必须管理发送缓冲池。 正确管理此类池需要预先分配足够的缓冲区空间来优化系统性能。

以下主题提供了有关协议驱动程序缓冲区管理、发送操作和接收操作的详细信息：

[协议驱动程序缓冲区管理](protocol-driver-buffer-management.md)

[从协议驱动程序发送数据](sending-data-from-a-protocol-driver.md)

[在协议驱动程序中接收数据](receiving-data-in-protocol-drivers.md)

 

