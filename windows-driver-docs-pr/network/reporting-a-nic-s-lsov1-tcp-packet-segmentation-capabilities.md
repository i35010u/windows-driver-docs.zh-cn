---
title: 报告的 NIC LSOV1 TCP 数据包分段功能
description: 报告的 NIC LSOV1 TCP 数据包分段功能
ms.assetid: 976f5943-a50e-413b-8520-e280b04122f9
keywords:
- LSOV1 WDK 网络
- 大型 TCP 数据包分段 WDK 网络
- 分段的大型 TCP 数据包 WDK 网络
- 任务卸载，WDK TCP/IP 传输，LSOV1 和 LSOV2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5af5c69dbc43f8718d44bbc68743ceb19f4a756f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56534427"
---
# <a name="reporting-a-nics-lsov1-tcp-packet-segmentation-capabilities"></a>报告的 NIC LSOV1 TCP 数据包分段功能





NDIS 微型端口驱动程序指定当前的大量发送卸载版本 1 (LSOV1)-TCP-数据包的分段配置中的 nic [ **NDIS\_TCP\_LARGE\_发送\_将卸载\_V1** ](https://msdn.microsoft.com/library/windows/hardware/ff567883)结构。微型端口驱动程序必须包括中的当前 LSOV1 卸载配置[ **NDIS\_微型端口\_适配器\_卸载\_特性**](https://msdn.microsoft.com/library/windows/hardware/ff565930)结构。 微型端口驱动程序调用[ **NdisMSetMiniportAttributes** ](https://msdn.microsoft.com/library/windows/hardware/ff563672)函数从[ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)函数并传递中信息在 NDIS\_微型端口\_适配器\_卸载\_属性。

微型端口驱动程序必须报告 LSOV1 配置中的更改，如果有，请在[ **NDIS\_状态\_任务\_卸载\_当前\_配置**](https://msdn.microsoft.com/library/windows/hardware/ff567424)状态指示。

中的查询响应[OID\_TCP\_卸载\_当前\_CONFIG](https://msdn.microsoft.com/library/windows/hardware/ff569805)，NDIS 包括 NDIS\_TCP\_大\_发送\_将卸载\_V1 中的结构[ **NDIS\_卸载**](https://msdn.microsoft.com/library/windows/hardware/ff566599) NDIS 返回中的结构**InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构。 NDIS 使用微型端口驱动程序提供的信息。

NDIS 支持大量发送卸载版本 2 (LSOV2) 是 LSO 的增强的版本。 有关 LSOV2 功能的详细信息，请参阅[报告的 NIC LSOV2 TCP 数据包分段功能](reporting-a-nic-s-lsov2-tcp-packet-segmentation-capabilities.md)。

微型端口驱动程序必须指定以下信息在 NDIS\_TCP\_LARGE\_发送\_卸载\_V1 结构：

-   封装设置，请在**封装**成员。 有关此成员的详细信息，请参阅中的备注部分[ **NDIS\_TCP\_LARGE\_发送\_卸载\_V1**](https://msdn.microsoft.com/library/windows/hardware/ff567883)。

-   TCP/IP 传输在中可以传递给一个大型的 TCP 数据包中的微型端口驱动程序的用户数据的最大字节数**MaxOffLoadSize**成员。 最大大小不能超过 64k 字节。

-   TCP/IP 传输可以将卸载它为分段的 nic 中之前，大型的 TCP 数据包必须能被整除的段的最小数目**MinSegmentCount**成员。

-   NIC 可分段大的 TCP 数据包是否包含 TCP 选项。

-   NIC 可分段大的 TCP 数据包是否包含 IPv4 选项。

## <a name="related-topics"></a>相关主题


[确定任务卸载功能](determining-task-offload-capabilities.md)

 

 






