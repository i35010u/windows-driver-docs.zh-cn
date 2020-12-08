---
title: NDIS 6.30 后向兼容性
description: NDIS 6.30 向向后兼容的功能添加了适用于 NDIS 6.20 和 NDIS 6.0 驱动程序的功能。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f95d8982f1405c039ea3a8755ae4cf80b50e80e2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96798035"
---
# <a name="ndis-630-backward-compatibility"></a>NDIS 6.30 后向兼容性


NDIS 6.30 向向后兼容的功能添加了适用于 NDIS 6.20 和 NDIS 6.0 驱动程序的功能。 有关 NDIS 6.20 兼容性问题的信息，请参阅 [ndis 6.20 向后兼容性](ndis-6-20-backward-compatibility.md)。 有关 NDIS 6.0 兼容性问题的信息，请参阅 [ndis 6.0 向后兼容性](/previous-versions/windows/hardware/network/ndis-6-0-backward-compatibility)。

有关 NDIS 6.30 功能的详细信息，请参阅 [ndis 6.30 简介](introduction-to-ndis-6-30.md)。

## <a name="features-that-are-no-longer-supported"></a>不再受支持的功能


Windows 8 及更高版本不支持以下功能：

-   虚拟机不再支持 TCP 烟囱卸载。 但是，它仍支持本机使用。
-   [IPsec 任务卸载版本 1](background-reading-on-ipsec.md)。 应更新支持 IPsec 任务卸载的所有驱动程序，以支持 [ipsec 任务卸载版本 2](./introduction-to-ipsec-offload-version-2.md)。
-   筛选中间驱动程序。 相反，请使用 NDIS 6。*x* 筛选器驱动程序接口。 有关筛选器驱动程序的详细信息，请参阅 [NDIS 筛选器驱动程序](ndis-filter-drivers.md)。
-   802.11 用于模拟802.3 的驱动程序。 NDIS 802.11 驱动程序必须支持本机802.11 接口。 有关本机802.11 的详细信息，请参阅 [本机802.11 无线 LAN](/previous-versions/windows/hardware/wireless/ff560689(v=vs.85))。
-   NDIS WAN 驱动程序。 NDIS WAN 驱动程序必须移植到 NDIS 6.0 CoNDIS WAN 驱动程序模型。 有关 CoNDIS WAN 的详细信息，请参阅 [Wan 微型端口驱动程序](wan-miniport-drivers.md)。

## <a name="features-that-have-been-removed"></a>已删除的功能


Windows 8 及更高版本中已删除以下功能：

-   NDIS 1.x 和更早版本
-   IrDA 微型端口驱动程序
-   NetDMA
-   令牌环 (802.5) 

## <a name="other-changes"></a>其他更改


-   Windows 8 随附的 TCP/IP 协议驱动程序已更新为 NDIS 6.30。 但是，此更改相对较小，因此，只需移植驱动程序即可实现此功能。 TCP/IP 协议驱动程序与驱动程序堆栈中的 NDIS 6.20 和更早的驱动程序向后兼容。

 

