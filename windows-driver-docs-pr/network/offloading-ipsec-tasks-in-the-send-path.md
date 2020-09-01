---
title: 在发送路径中卸载 IPsec 任务
description: 在发送路径中卸载 IPsec 任务
ms.assetid: b95878e0-0aee-43cb-a64c-b5d8e07cb1b4
keywords:
- 受 ESP 保护的数据包 WDK IPsec 卸载、发送路径卸载
- 受 AH 保护的数据包 WDK IPsec 卸载、发送路径卸载
- 发送路径卸载 WDK IPsec 卸载
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 23a482a98a62a985b2438129fa9ff1d1676c540f
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89217529"
---
# <a name="offloading-ipsec-tasks-in-the-send-path"></a>在发送路径中卸载 IPsec 任务

\[IPsec 任务卸载功能已弃用，不应使用。\]




在将 TCP/IP 传输传递到微型端口驱动程序的 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list) 结构（NIC 将 (IPsec) 任务执行 Internet 协议安全）之前，它将更新与网络 \_ 缓冲区列表结构关联的 IPsec 信息 \_ 。 TCP/IP 传输在 [**NDIS \_ IPSEC \_ 卸载 \_ V1 \_ 网络 \_ 缓冲区 \_ 列表 \_ 信息**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_ipsec_offload_v1_net_buffer_list_info) 结构中指定此信息，这是网络 \_ 缓冲区 \_ 列表信息 (带外数据) 的一部分，与网络 \_ 缓冲区 \_ 列表结构关联。

TCP/IP 传输提供 *OffloadHandle*，该协议指定发送数据包的端到端连接) 部分传输 (出站 SA 的句柄。 如果数据包将通过隧道传输，则 TCP/IP 传输还会提供 *NextOffloadHandle*，它为发送数据包的隧道部分指定出站 SA 的句柄。

当微型端口驱动程序在其[*MiniportSendNetBufferLists*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_send_net_buffer_lists)或[**MiniportCoSendNetBufferLists**](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_co_send_net_buffer_lists)函数中收到[**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构后，它可以调用* \_ Id*为**IPsecOffloadV1NetBufferListInfo**的[**网络 \_ 缓冲区 \_ 列表 \_ 信息**](/windows-hardware/drivers/ddi/ndis/nf-ndis-net_buffer_list_info)宏，以获取 \_ \_ \_ \_ \_ \_ \_ 与网络 \_ 缓冲区 \_ 列表结构关联的 NDIS IPSEC 卸载 V1 网络缓冲区列表信息结构。

当 NIC 在发送数据包上执行 IPsec 处理时，它会为数据包计算 (或两个) 的 AH 或 ESP 加密校验和，如果数据包包含 ESP 有效负载，则会对数据包进行加密。 TCP/IP 传输已经将数据包括起来， (如有必要) ，并为其分配一个序列号和 SPI。

 

