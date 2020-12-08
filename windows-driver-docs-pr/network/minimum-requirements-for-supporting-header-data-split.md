---
title: 标头数据拆分的最低支持要求
description: 标头数据拆分的最低支持要求
keywords:
- 标头-数据拆分 WDK，要求
- 以太网帧拆分 WDK 网络，要求
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 40dc55ee9de29795079957dfdce588371330777d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96798085"
---
# <a name="minimum-requirements-for-supporting-header-data-split"></a>标头数据拆分的最低支持要求





本主题概述了提供程序支持标头数据拆分所必须满足的最低要求。 有关适用于拆分以太网帧的规则的完整列表，请参阅 [拆分以太网帧](splitting-ethernet-frames.md)。

下面的列表包含对标头数据拆分支持的最低要求：

-   [如果未使用 Header-Data split 的情况](cases-where-header-data-split-is-not-used.md)，则提供程序不能拆分框架。

-   提供程序必须将虚拟 LAN (VLAN) 标记移动到 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list) 结构 OOB 数据。 有关 VLAN 要求的详细信息，请参阅 [接收具有 Header-Data 拆分的指示](receive-indications-with-header-data-split.md)。

-   提供程序必须支持不带选项拆分 IPv4 帧。 有关拆分 IPv4 帧的详细信息，请参阅 [拆分 Ipv4 帧](splitting-ipv4-frames.md)。

-   提供程序必须支持不含扩展标头的拆分 IPv6 帧。 有关拆分 IPv6 帧的详细信息，请参阅 [拆分 Ipv6 帧](splitting-ipv6-frames.md)。

-   提供程序必须支持在 TCP 负载中拆分 TCP 帧，无需 TCP 选项，且仅支持 timestamp 选项。 有关拆分 TCP 帧的详细信息，请参阅 [在 Tcp 负载处拆分帧](splitting-frames-at-the-tcp-payload.md)。

-   提供程序必须支持在 UDP 负载处拆分 UDP 帧。 有关拆分 UDP 帧的详细信息，请参阅 [在 Udp 有效负载下拆分框架](splitting-frames-at-the-udp-payload.md)。

-   提供程序必须支持标头数据拆分初始化属性。 有关这些属性的详细信息，请参阅 [初始化 Header-Data 拆分提供程序](initializing-a-header-data-split-provider.md)。

-   提供程序必须支持标头数据拆分接收指示要求，包括在 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构的 **NblFlags** 成员中设置标头数据拆分标志、标头大小要求和数据回填要求。 有关接收要求的详细信息，请参阅 [接收具有 Header-Data 拆分的指示](receive-indications-with-header-data-split.md)。

-   提供程序必须支持 [oid \_ gen \_ hd \_ Split \_ PARAMETERS](./oid-gen-hd-split-parameters.md) oid、 [oid \_ gen \_ hd \_ split \_ 当前 \_ 配置](./oid-gen-hd-split-current-config.md) oid、 [**NDIS \_ 状态 \_ hd \_ split \_ 当前 \_ 配置**](./ndis-status-hd-split-current-config.md) 状态指示和注册表设置。 有关标头-数据拆分参数和设置的详细信息，请参阅 [标头-数据拆分管理和配置](setting-the-current-header-data-split-configuration.md)。

有关协议驱动程序和筛选器驱动程序的标头数据拆分要求的详细信息，请参阅 [支持 Header-Data 剥离协议驱动程序和筛选器驱动](supporting-header-data-split-in-protocol-driver-and-filter-drivers.md)程序。

 

