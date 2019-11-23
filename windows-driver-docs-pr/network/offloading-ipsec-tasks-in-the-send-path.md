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
ms.openlocfilehash: 762ff85b05589f46367f6fa4e1ed20a8c1934cdb
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834614"
---
# <a name="offloading-ipsec-tasks-in-the-send-path"></a>在发送路径中卸载 IPsec 任务

\[IPsec 任务卸载功能已弃用，不应使用。\]




在将 TCP/IP 传输传递到微型端口驱动程序之前，[**网络\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构中 NIC 将在其上执行 Internet 协议安全（IPsec）任务的数据包将更新与 NET\_缓冲区关联的 IPsec 信息\_列表结构。 TCP/IP 传输在[**NDIS\_IPSEC\_卸载中指定此信息\_V1\_NET\_buffer\_list\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_ipsec_offload_v1_net_buffer_list_info)结构，它是与 NET\_BUFFER\_list 结构关联的 NET\_缓冲区\_列表信息（带外数据）的一部分。

TCP/IP 传输提供*OffloadHandle*，它指定发送数据包的传输（端到端连接）部分的出站 SA 的句柄。 如果数据包将通过隧道传输，则 TCP/IP 传输还会提供*NextOffloadHandle*，它为发送数据包的隧道部分指定出站 SA 的句柄。

当微型端口驱动程序在其[*MiniportSendNetBufferLists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_send_net_buffer_lists)或[**MiniportCoSendNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_co_send_net_buffer_lists)函数中收到[**NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构时，它可以使用 *\_ID* **IPsecOffloadV1NetBufferListInfo**调用[**NET\_缓冲区\_列表\_info**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-info)宏，以获取 NDIS\_\_\_\_\_\_\_与 NET\_缓冲区关联\_列表结构。

当 NIC 对发送数据包执行 IPsec 处理时，它会为数据包计算 AH 或 ESP 加密校验和，如果数据包包含 ESP 有效负载，则会对数据包进行加密。 TCP/IP 传输已经将数据包括起来，并将其填充（如有必要），并为其分配了序列号和 SPI。

 

 





