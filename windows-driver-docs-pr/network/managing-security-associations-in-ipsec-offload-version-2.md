---
title: 管理 IPsec 卸载版本 2 中的安全关联
description: 管理 IPsec 卸载版本 2 中的安全关联
ms.assetid: aaa352c1-fb70-4c96-adda-9710347e2442
keywords:
- IPsecOV2 WDK TCP/IP 传输，安全关联
- 安全关联 WDK IPsec 卸载
- SAs WDK IPsec 卸载
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4c416082242bb24a5b147886072d228d95fa0a20
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89213945"
---
# <a name="managing-security-associations-in-ipsec-offload-version-2"></a>管理 IPsec 卸载版本 2 中的安全关联

\[IPsec 任务卸载功能已弃用，不应使用。\]




TCP/IP 传输确定 NIC 可以执行 IPsec 卸载版本 2 (IPsecOV2) 操作时 (参阅 [报告 nic 的 Ipsec 卸载版本2功能](reporting-a-nic-s-ipsec-offload-version-2-capabilities.md)) ，传输请求 NIC 的微型端口驱动程序将 SAs (中的一个或多个安全关联添加到 nic，然后传输才能将 IPsec 任务卸载到 nic。 添加 SAs 后，TCP/IP 传输还可以删除或更新它们。 IPsecOV2 接口需要用于添加、删除和更新 Oid 的 NDIS 直接 OID 接口。

**注意**   NDIS 为 NDIS 6.1 和更高版本的驱动程序提供直接 OID 请求接口。 [直接 OID 请求路径](/windows-hardware/drivers/ddi/_netvista/)支持经常查询或设置的 OID 请求。

 

若要请求微型端口驱动程序将一个或多个 SAs 添加到 NIC，TCP/IP 传输会设置 [OID \_ TCP 任务 \_ " \_ IPSEC \_ 卸载 \_ V2 \_ 添加 \_ SA](./oid-tcp-task-ipsec-offload-v2-add-sa.md) OID"。 微型端口驱动程序接收 [**IPSEC \_ 卸载 \_ V2 \_ 添加 \_ SA**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ipsec_offload_v2_add_sa) 结构，并为 SA 配置用于 IPsecOV2 处理的 NIC。 如果成功设置为 OID \_ TCP \_ 任务 \_ IPSEC \_ 卸载 \_ v2 \_ ADD \_ SA，微型端口驱动程序将初始化一个句柄，该句柄在 IPSEC \_ 卸载 \_ V2 \_ 添加 \_ SA 结构中标识卸载的 SA。 传输将对微型端口驱动程序的后续请求中使用此句柄 (也就是说，在发送路径上或在调用中修改或删除 SA) 。 有关使用发送路径中的 SA 句柄的详细信息，请参阅使用 [IPsec 卸载版本2发送网络数据](sending-network-data-with-ipsec-offload-version-2.md)。

微型端口驱动程序报告 NIC 在[**NDIS \_ IPSEC \_ 卸载 \_ V2**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_ipsec_offload_v2)结构的**SaOffloadCapacity**成员中可以支持的 SAs 的数目。

微型端口驱动程序可以在[**NDIS \_ IPSEC \_ 卸载 \_ V2 \_ 网络 \_ 缓冲区 \_ 列表 \_ 信息**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_ipsec_offload_v2_net_buffer_list_info)结构中设置接收数据包的**SaDeleteReq**标志。 接下来，TCP/IP 传输会发出 [OID \_ TCP \_ 任务 \_ IPSEC \_ 卸载 \_ V2 \_ delete \_ SA](./oid-tcp-task-ipsec-offload-v2-delete-sa.md) ，以便删除接收数据包的入站 sa，并再次删除与已删除的入站 sa 相对应的出站 sa。

TCP/IP 传输颁发 [OID \_ TCP \_ 任务 \_ IPSEC \_ 卸载 \_ V2 \_ 删除 \_ ](./oid-tcp-task-ipsec-offload-v2-delete-sa.md) 接收数据包的入站 sas，并删除与已删除的入站 sas 相对应的出站 sas。 NIC 在接收相应的 OID \_ TCP \_ 任务 \_ IPSEC \_ 卸载 \_ V2 \_ \_ 请求之前，不能删除这些 SAs。

TCP/IP 传输设置 [OID \_ TCP \_ 任务 \_ IPSEC \_ 卸载 \_ V2 \_ 更新 \_ SA](./oid-tcp-task-ipsec-offload-v2-update-sa.md) OID，请求微型端口驱动程序使用扩展序列号 (ESN) 的 SA 更新具有更高顺序位的 NIC。 对于支持 ESN 的 Nic，当微型端口驱动程序收到此请求时，驱动程序应根据 Ipsec 卸载 v2 [** \_ \_ \_ 更新 \_ SA**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ipsec_offload_v2_update_sa)结构的**操作**成员中指定的[**ipsec \_ 卸载 \_ v2 \_ 操作**](/windows-hardware/drivers/ddi/ndis/ne-ndis-_ipsec_offload_v2_operation)枚举值更新 NIC 中指定 SA 的序列号。

 

