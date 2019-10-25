---
title: NDIS 6.20 中的媒体可扩展性
description: NDIS 6.20 中的媒体可扩展性
ms.assetid: abc240da-be6e-4a7a-a9d1-186633c5bfd3
keywords:
- NDIS 6.20 WDK，媒体扩展性
- 媒体扩展 WDK NDIS 6.20
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7e2fe7f34974a03acb9213717be402e32ecd8594
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844266"
---
# <a name="media-extensibility-in-ndis-620"></a>NDIS 6.20 中的媒体可扩展性





NDIS 6.20 引入了其他媒体扩展功能。 也就是说，驱动程序堆栈的网络层是独立于介质的。

在 NDIS 6.20 和更高版本中，这些功能降低了实现不实现 IEEE 802.3 的驱动程序所需的代码的复杂性。 此外，这些非 IEEE 802.3 实现不需要实现 ARP 和 DHCP。

NDIS 6.20 和更高版本使用原始 ip （NdisMediumIP）的新媒体类型提供*原始 ip*帧支持。 例如，NDIS WWAN 支持使用原始 IP。

NDIS 6.20 增强了对特定于媒体的带外（OOB）数据的支持。 媒体特定信息具有 Microsoft 分配的标记。 NDIS 6.20 和更高版本支持多个媒体特定的信息标记。

有关媒体特定信息的详细信息，请参阅[OID\_GEN\_物理\_中型\_EX](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-physical-medium-ex)和[**NDIS\_NBL\_\_特定\_媒体信息\_例如**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_nbl_media_specific_information_ex)

 

 





