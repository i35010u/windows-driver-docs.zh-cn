---
title: NDIS 6.20 的媒体可扩展性
description: NDIS 6.20 的媒体可扩展性
ms.assetid: abc240da-be6e-4a7a-a9d1-186633c5bfd3
keywords:
- NDIS 6.20 WDK，媒体扩展性
- 媒体扩展性 WDK NDIS 6.20
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ea8345740d9d5b8359369394f1fb69f5b7ddeab9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56545531"
---
# <a name="media-extensibility-in-ndis-620"></a>NDIS 6.20 的媒体可扩展性





NDIS 6.20 引入了其他媒体扩展功能。 也就是说，驱动程序堆栈的网络层是更多的独立媒体。

NDIS 6.20 及更高版本的这些功能降低实现未实现 IEEE 802.3 的驱动程序所需的代码的复杂性。 此外，这些非 IEEE 802.3 实现无需实现 ARP 和 DHCP。

NDIS 6.20 及更高版本提供*原始 IP*对原始 IP (NdisMediumIP) 帧具有新的媒体类型的支持。 例如，NDIS WWAN 支持使用原始 IP。

NDIS 6.20 引入了对媒体特定带外 (OOB) 数据的增强的支持。 媒体特定信息具有 Microsoft 分配的标记。 NDIS 6.20 及更高版本支持多个媒体的特定信息标记。

有关媒体的特定信息，详细了解媒体扩展的详细信息请参阅[OID\_代\_物理\_中等\_EX](https://msdn.microsoft.com/library/windows/hardware/ff569622)和[**NDIS\_NBL\_媒体\_特定\_信息\_EX**](https://msdn.microsoft.com/library/windows/hardware/ff566518)。

 

 





