---
title: NDIS 6.20 中的媒体可扩展性
description: NDIS 6.20 中的媒体可扩展性
keywords:
- NDIS 6.20 WDK，媒体扩展性
- 媒体扩展 WDK NDIS 6.20
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2382784e904807ebe0405593c4864ff307a511d7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803679"
---
# <a name="media-extensibility-in-ndis-620"></a>NDIS 6.20 中的媒体可扩展性





NDIS 6.20 引入了其他媒体扩展功能。 也就是说，驱动程序堆栈的网络层是独立于介质的。

在 NDIS 6.20 和更高版本中，这些功能降低了实现不实现 IEEE 802.3 的驱动程序所需的代码的复杂性。 此外，这些非 IEEE 802.3 实现不需要实现 ARP 和 DHCP。

NDIS 6.20 和更高版本使用原始 ip (NdisMediumIP) 的新媒体类型为 *原始 ip* 帧提供支持。 例如，NDIS WWAN 支持使用原始 IP。

NDIS 6.20 为特定于媒体的带外 (OOB) 数据引入了增强支持。 媒体特定信息具有 Microsoft 分配的标记。 NDIS 6.20 和更高版本支持多个媒体特定的信息标记。

有关媒体特定信息的详细信息，请参阅 [OID \_ GEN \_ 实地 \_ MEDIUM \_ EX](./oid-gen-physical-medium-ex.md) 和 [**NDIS \_ NBL \_ media \_ 特定 \_ 信息， \_ 例如**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_nbl_media_specific_information_ex)：

 

