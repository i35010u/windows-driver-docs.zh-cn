---
title: NDIS 6.20 中的媒体可扩展性
description: NDIS 6.20 中的媒体可扩展性
ms.assetid: abc240da-be6e-4a7a-a9d1-186633c5bfd3
keywords:
- NDIS 6.20 WDK，媒体扩展性
- 媒体扩展性 WDK NDIS 6.20
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7364adcd5a0eccf5175322d0941b74b0a0bdd8a1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373988"
---
# <a name="media-extensibility-in-ndis-620"></a>NDIS 6.20 中的媒体可扩展性





NDIS 6.20 引入了其他媒体扩展功能。 也就是说，驱动程序堆栈的网络层是更多的独立媒体。

NDIS 6.20 及更高版本的这些功能降低实现未实现 IEEE 802.3 的驱动程序所需的代码的复杂性。 此外，这些非 IEEE 802.3 实现无需实现 ARP 和 DHCP。

NDIS 6.20 及更高版本提供*原始 IP*对原始 IP (NdisMediumIP) 帧具有新的媒体类型的支持。 例如，NDIS WWAN 支持使用原始 IP。

NDIS 6.20 引入了对媒体特定带外 (OOB) 数据的增强的支持。 媒体特定信息具有 Microsoft 分配的标记。 NDIS 6.20 及更高版本支持多个媒体的特定信息标记。

有关媒体的特定信息，详细了解媒体扩展的详细信息请参阅[OID\_代\_物理\_中等\_EX](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-physical-medium-ex)和[**NDIS\_NBL\_媒体\_特定\_信息\_EX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_nbl_media_specific_information_ex)。

 

 





