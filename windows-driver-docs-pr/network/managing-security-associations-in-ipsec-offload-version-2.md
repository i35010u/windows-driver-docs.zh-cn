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
ms.openlocfilehash: 1f269b97f1c82ad011ed87b3177150bfd272de94
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844113"
---
# <a name="managing-security-associations-in-ipsec-offload-version-2"></a>管理 IPsec 卸载版本 2 中的安全关联

\[IPsec 任务卸载功能已弃用，不应使用。\]




在 TCP/IP 传输确定 NIC 可以执行 IPsec 卸载版本2（IPsecOV2）操作（请参阅[报告 nic 的 Ipsec 卸载版本2功能](reporting-a-nic-s-ipsec-offload-version-2-capabilities.md)）后，传输请求 nic 的微型端口驱动程序添加一个或多个安全性在传输前将 IPsec 任务卸载到 NIC 之前，可以将 IPsec 任务卸载到 nic。 添加 SAs 后，TCP/IP 传输还可以删除或更新它们。 IPsecOV2 接口需要用于添加、删除和更新 Oid 的 NDIS 直接 OID 接口。

**请注意**  NDIS 为 ndis 6.1 和更高版本的驱动程序提供直接 OID 请求接口。 [直接 OID 请求路径](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)支持经常查询或设置的 OID 请求。

 

若要请求微型端口驱动程序将一个或多个 SAs 添加到 NIC，TCP/IP 传输[\_tcp\_任务将 OID 设置\_IPSEC\_卸载\_V2\_添加\_SA](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-task-ipsec-offload-v2-add-sa) OID。 微型端口驱动程序接收[**IPSEC\_卸载\_V2\_添加\_sa**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ipsec_offload_v2_add_sa)结构，并为 Sa 配置 IPsecOV2 处理的 NIC。 成功设置到 OID 后\_TCP\_任务\_IPSEC\_卸载\_V2\_添加\_SA，微型端口驱动程序初始化一个句柄，该句柄在 IPSEC\_卸载中标识卸载的 SA\_V2\_添加\_SA 结构。 传输在对微型端口驱动程序的后续请求中使用此句柄（即，在发送路径上或在调用中修改或删除 SA）。 有关使用发送路径中的 SA 句柄的详细信息，请参阅使用[IPsec 卸载版本2发送网络数据](sending-network-data-with-ipsec-offload-version-2.md)。

小型端口驱动程序在[**NDIS\_IPSEC\_卸载\_V2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_ipsec_offload_v2)结构的**SaOffloadCapacity**成员中报告 NIC 可以支持的 SAs 的数目。

小型端口驱动程序可以在[**NDIS\_IPSEC\_卸载\_\_V2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_ipsec_offload_v2_net_buffer_list_info)中设置**SaDeleteReq**标志，以接收数据包\_\_\_ 接下来，TCP/IP 传输[\_tcp\_任务发送 OID，\_IPSEC\_卸载\_V2\_删除\_SA](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-task-ipsec-offload-v2-delete-sa)一次以删除数据包的入站 SA，并再次删除与已删除的入站 SA 相对应的出站 SA。

TCP/IP 传输问题[\_tcp\_任务\_IPSEC\_卸载\_V2\_delete\_SA](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-task-ipsec-offload-v2-delete-sa)删除接收数据包时使用的入站 sas，并删除与已删除入站 SAs。 NIC 在收到相应 OID 之前，不能删除这些 SAs\_TCP\_任务\_IPSEC\_卸载\_V2\_DELETE\_SA 请求。

TCP/IP 传输[\_tcp\_任务将 OID 设置为 tcp 任务\_IPSEC\_卸载\_V2\_更新\_SA](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-task-ipsec-offload-v2-update-sa) OID，请求微型端口驱动程序使用扩展序列号（ESN）。 对于支持 ESN 的 Nic，当微型端口驱动程序收到此请求时，驱动程序应根据[**IPSEC\_卸载\_V2\_操作**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ne-ndis-_ipsec_offload_v2_operation)枚举值更新 NIC 中指定 SA 的序列号在[**IPSEC\_卸载\_V2\_UPDATE\_SA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ipsec_offload_v2_update_sa)结构的**操作**成员中指定的。

 

 





