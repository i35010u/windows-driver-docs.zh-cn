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
ms.openlocfilehash: deecaf4b56ddcf841a0b38fed885a0504e2a9657
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564222"
---
# <a name="managing-security-associations-in-ipsec-offload-version-2"></a>管理 IPsec 卸载版本 2 中的安全关联

\[IPsec 任务卸载功能已弃用，不应使用。\]




后 TCP/IP 传输确定 NIC 可以执行 IPsec 卸载版本 2 (IPsecOV2) 操作 (请参阅[报告 NIC 的 IPsec 卸载版本 2 功能](reporting-a-nic-s-ipsec-offload-version-2-capabilities.md))，NIC 的微型端口驱动程序添加一个传输请求或更多安全关联 (Sa) 之前传输的 nic 可以 IPsec 将任务卸载到 nic。 添加后 SAs，TCP/IP 传输还可以删除或更新它们。 IPsecOV2 接口需要 NDIS 直接 OID 接口以进行添加、 删除和更新 Oid。

**请注意**  NDIS NDIS 6.1 和更高版本的驱动程序提供直接的 OID 请求接口。 [直接 OID 请求路径](https://msdn.microsoft.com/library/windows/hardware/ff564736)支持查询或频繁设置的 OID 请求。

 

以请求微型端口驱动程序向 NIC，TCP/IP 传输集添加一个或多个 SAs [OID\_TCP\_任务\_IPSEC\_卸载\_V2\_添加\_SA](https://msdn.microsoft.com/library/windows/hardware/ff569812) OID。 微型端口驱动程序收到[ **IPSEC\_卸载\_V2\_添加\_SA** ](https://msdn.microsoft.com/library/windows/hardware/ff556977)结构，并配置对 SA 处理 IPsecOV2 的 NIC。 成功设置为 OID\_TCP\_任务\_IPSEC\_卸载\_V2\_添加\_SA，微型端口驱动程序初始化标识中卸载的 SA 的句柄IPSEC\_卸载\_V2\_添加\_SA 结构。 传输到微型端口驱动程序的后续请求中使用此句柄 (即发送路径上或在调用中修改或删除 SA)。 有关在发送路径中使用的 SA 句柄的详细信息，请参阅[IPsec 卸载版本 2 发送网络数据](sending-network-data-with-ipsec-offload-version-2.md)。

微型端口驱动程序报告可以支持中的 NIC 的 Sa 数量**SaOffloadCapacity**的成员[ **NDIS\_IPSEC\_卸载\_V2**](https://msdn.microsoft.com/library/windows/hardware/ff565808)结构。

微型端口驱动程序可以设置**SaDeleteReq**中的标志[ **NDIS\_IPSEC\_卸载\_V2\_NET\_缓冲区\_列表\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff565818)接收数据包的结构。 TCP/IP 传输随后发出[OID\_TCP\_任务\_IPSEC\_卸载\_V2\_删除\_SA](https://msdn.microsoft.com/library/windows/hardware/ff569813)一次，以删除通过接收数据包的入站的 SA，一次试删除对应于已删除的入站 SA 的出站 SA。

TCP/IP 传输问题[OID\_TCP\_任务\_IPSEC\_卸载\_V2\_删除\_SA](https://msdn.microsoft.com/library/windows/hardware/ff569813)若要删除的入站的 SAs接收数据包，删除对应于已删除的入站 SAs 的出站 Sa。 NIC 必须删除这些 SAs 才能收到相应的 OID\_TCP\_任务\_IPSEC\_卸载\_V2\_删除\_SA 请求。

TCP/IP 传输集[OID\_TCP\_任务\_IPSEC\_卸载\_V2\_更新\_SA](https://msdn.microsoft.com/library/windows/hardware/ff569814) OID 以请求微型端口驱动程序更新 NIC 具有较高顺序位扩展的序列号 (ESN) sa。 为支持 ESN，Nic 驱动程序微型端口驱动程序接收此请求时，应更新指定的 SA，根据所使用的 nic 的序列号[ **IPSEC\_卸载\_V2\_操作**](https://msdn.microsoft.com/library/windows/hardware/ff556984)中指定的枚举值**操作**的成员[ **IPSEC\_卸载\_V2\_更新\_SA** ](https://msdn.microsoft.com/library/windows/hardware/ff556990)结构。

 

 





