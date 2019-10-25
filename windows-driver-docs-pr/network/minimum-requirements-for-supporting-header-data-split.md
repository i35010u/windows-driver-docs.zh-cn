---
title: 标头数据拆分的最低支持要求
description: 标头数据拆分的最低支持要求
ms.assetid: 32ca214a-5103-4472-bbdb-1338188750d9
keywords:
- 标头-数据拆分 WDK，要求
- 以太网帧拆分 WDK 网络，要求
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1fad56c53ebccc22e167768cf1aa009fd367cd62
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844261"
---
# <a name="minimum-requirements-for-supporting-header-data-split"></a>标头数据拆分的最低支持要求





本主题概述了提供程序支持标头数据拆分所必须满足的最低要求。 有关适用于拆分以太网帧的规则的完整列表，请参阅[拆分以太网帧](splitting-ethernet-frames.md)。

下面的列表包含对标头数据拆分支持的最低要求：

-   对于[不使用标头-数据拆分的情况](cases-where-header-data-split-is-not-used.md)，提供程序不得拆分框架。

-   提供程序必须将虚拟 LAN （VLAN）标记移动到[**NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构 OOB 数据。 有关 VLAN 要求的详细信息，请参阅[接收指示和标头-数据拆分](receive-indications-with-header-data-split.md)。

-   提供程序必须支持不带选项拆分 IPv4 帧。 有关拆分 IPv4 帧的详细信息，请参阅[拆分 Ipv4 帧](splitting-ipv4-frames.md)。

-   提供程序必须支持不含扩展标头的拆分 IPv6 帧。 有关拆分 IPv6 帧的详细信息，请参阅[拆分 Ipv6 帧](splitting-ipv6-frames.md)。

-   提供程序必须支持在 TCP 负载中拆分 TCP 帧，无需 TCP 选项，且仅支持 timestamp 选项。 有关拆分 TCP 帧的详细信息，请参阅[在 Tcp 负载处拆分帧](splitting-frames-at-the-tcp-payload.md)。

-   提供程序必须支持在 UDP 负载处拆分 UDP 帧。 有关拆分 UDP 帧的详细信息，请参阅[在 Udp 有效负载下拆分框架](splitting-frames-at-the-udp-payload.md)。

-   提供程序必须支持标头数据拆分初始化属性。 有关这些属性的详细信息，请参阅[初始化标头-数据拆分提供程序](initializing-a-header-data-split-provider.md)。

-   提供程序必须支持标头数据拆分接收指示要求，包括在[**网络\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)的**NblFlags**成员中设置标头数据拆分标志\_列表结构、标头大小要求和数据回填要求。 有关接收要求的详细信息，请参阅[接收指示和标头-数据拆分](receive-indications-with-header-data-split.md)。

-   提供程序必须支持[oid\_GEN\_HD\_拆分\_参数](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-hd-split-parameters)OID， [oid\_GEN\_HD\_拆分\_当前\_配置](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-hd-split-current-config)OID， [**NDIS\_状态\_hd\_拆分\_当前\_配置**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-hd-split-current-config)状态指示和注册表设置。 有关标头-数据拆分参数和设置的详细信息，请参阅[标头-数据拆分管理和配置](header-data-split-administration-and-configuration.md)。

有关协议驱动程序和筛选器驱动程序的标头数据拆分要求的详细信息，请参阅[在协议驱动程序和筛选器驱动程序中支持标头-数据拆分](supporting-header-data-split-in-protocol-driver-and-filter-drivers.md)。

 

 





