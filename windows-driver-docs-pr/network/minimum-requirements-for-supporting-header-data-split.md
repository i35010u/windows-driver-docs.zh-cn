---
title: 最低要求，以支持标头数据拆分
description: 最低要求，以支持标头数据拆分
ms.assetid: 32ca214a-5103-4472-bbdb-1338188750d9
keywords:
- 标头数据拆分 WDK，要求
- 以太网帧拆分 WDK 网络、 要求
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f06b029c1a4b5db1e96a0c37e5205b21bc56415f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524192"
---
# <a name="minimum-requirements-for-supporting-header-data-split"></a>最低要求，以支持标头数据拆分





本主题总结了提供程序支持标头数据拆分而必须满足的最低要求。 适用于拆分以太网帧的规则的完整列表，请参阅[拆分以太网帧](splitting-ethernet-frames.md)。

以下列表包含标头数据拆分支持的最低要求：

-   提供程序必须不拆分帧[情况下，标头数据拆分为不使用](cases-where-header-data-split-is-not-used.md)主题介绍。

-   提供程序必须将移动到的虚拟 LAN (VLAN) 标记[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388)结构 OOB 数据。 有关 VLAN 要求的详细信息，请参阅[标头数据拆分接收指示](receive-indications-with-header-data-split.md)。

-   提供程序必须支持不带选项的拆分 IPv4 帧。 有关拆分 IPv4 帧的详细信息，请参阅[拆分 IPv4 帧](splitting-ipv4-frames.md)。

-   提供程序必须支持拆分 IPv6 帧，而无需扩展标头。 有关拆分 IPv6 帧的详细信息，请参阅[拆分 IPv6 帧](splitting-ipv6-frames.md)。

-   提供程序必须支持拆分 TCP 帧 TCP 有效负载不带任何 TCP 选项以及通过仅的时间戳选项。 有关拆分 TCP 帧的详细信息，请参阅[拆分帧 TCP 有效负载](splitting-frames-at-the-tcp-payload.md)。

-   提供程序必须支持拆分 UDP 帧的 UDP 负载。 有关拆分 UDP 帧的详细信息，请参阅[UDP 负载拆分帧](splitting-frames-at-the-udp-payload.md)。

-   提供程序必须支持标头数据拆分初始化属性。 有关这些属性的详细信息，请参阅[初始化标头数据拆分提供程序](initializing-a-header-data-split-provider.md)。

-   提供程序必须支持标头数据拆分接收指示要求，包括设置标头数据拆分中的标志**NblFlags**的成员[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388)结构、 标头大小要求以及数据回填要求。 有关详细信息接收要求，请参阅[标头数据拆分接收指示](receive-indications-with-header-data-split.md)。

-   提供程序必须支持[OID\_代\_HD\_拆分\_参数](https://msdn.microsoft.com/library/windows/hardware/ff569587)OID， [OID\_常规\_HD\_拆分\_当前\_CONFIG](https://msdn.microsoft.com/library/windows/hardware/ff569586) OID， [ **NDIS\_状态\_HD\_拆分\_当前\_配置**](https://msdn.microsoft.com/library/windows/hardware/ff567370)状态指示和注册表设置。 有关标头数据拆分参数和设置的详细信息，请参阅[标头数据拆分管理和配置](header-data-split-administration-and-configuration.md)。

关于协议驱动程序和筛选器驱动程序的标头数据拆分要求的详细信息，请参阅[协议驱动程序和筛选器驱动程序中支持标头数据拆分](supporting-header-data-split-in-protocol-driver-and-filter-drivers.md)。

 

 





