---
title: 从 NIC 中删除安全关联
description: 从 NIC 中删除安全关联
ms.assetid: 739a3fef-f0b4-4d7c-9d92-df52fd27915d
keywords:
- 安全关联 WDK IPsec 卸载
- SAs WDK IPsec 卸载
- 受 ESP 保护的数据包 WDK IPsec 卸载，安全关联
- 受 AH 保护的数据包 WDK IPsec 卸载，安全关联
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c8316581a4e1bc7295de90b0c5d4b6ba2b3546c6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834942"
---
# <a name="deleting-a-security-association-from-a-nic"></a>从 NIC 中删除安全关联

\[IPsec 任务卸载功能已弃用，不应使用。\]




如有必要，TCP/IP 传输可以将[OID\_TCP\_任务\_IPSEC\_delete\_SA](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-task-ipsec-delete-sa)来请求微型端口驱动程序从 NIC 删除安全关联（SA）。

若要为 NIC 上的另一个 SA 创建空间，小型端口驱动程序可以在 NDIS 中设置**SaDeleteReq**标志[ **\_IPSEC\_卸载\_V1\_NET\_BUFFER\_列出接收数据包\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_ipsec_offload_v1_net_buffer_list_info)结构。 接下来，TCP/IP 传输\_\_TCP 任务\_IPSEC\_删除\_SA，以便删除接收数据包的入站安全关联（SA），另一次则删除出站 SA对应于已删除的入站 SA。 NIC 在收到相应 OID 之前，不能删除其中的任何一种 SAs\_TCP\_任务\_IPSEC\_DELETE\_SA 请求。 微型端口驱动程序可以独立于**CryptoDone**标志来设置**SaDeleteReq** 。
