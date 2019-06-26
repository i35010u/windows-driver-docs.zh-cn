---
title: 从 NIC 中删除安全关联
description: 从 NIC 中删除安全关联
ms.assetid: 739a3fef-f0b4-4d7c-9d92-df52fd27915d
keywords:
- 安全关联 WDK IPsec 卸载
- SAs WDK IPsec 卸载
- ESP 保护数据包 WDK IPsec 卸载、 安全关联
- AH 保护数据包 WDK IPsec 卸载、 安全关联
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c07e4765913047acd5a10d654cc09480f5e2d581
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379219"
---
# <a name="deleting-a-security-association-from-a-nic"></a>从 NIC 中删除安全关联

\[IPsec 任务卸载功能已弃用，不应使用。\]




如果有必要，请 TCP/IP 传输可以设置[OID\_TCP\_任务\_IPSEC\_删除\_SA](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-task-ipsec-delete-sa)以请求微型端口驱动程序删除安全关联 (SA)从 nic。

若要创建的 NIC 上的另一个 SA 空间，微型端口驱动程序可以设置**SaDeleteReq**中的标志[ **NDIS\_IPSEC\_卸载\_V1\_NET\_缓冲区\_列表\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_ipsec_offload_v1_net_buffer_list_info)接收数据包的结构。 TCP/IP 传输随后发出 OID\_TCP\_任务\_IPSEC\_删除\_SA 一次，以删除通过接收数据包的入站的安全关联 (SA) 和另一个时间删除对应于已删除的入站 SA 的出站 SA。 NIC 必须删除这些 SAs 之一才能收到相应的 OID\_TCP\_任务\_IPSEC\_删除\_SA 请求。 微型端口驱动程序可以设置**SaDeleteReq**独立于**CryptoDone**标志。
