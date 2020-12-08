---
title: 严格优先级算法
description: 严格优先级算法
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f95f4311c51ea970c951427ad0dd4db72336b7f9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96824983"
---
# <a name="strict-priority-algorithm"></a>严格优先级算法


严格优先级是 (的 TSA) 的传输选择算法，该算法是在 IEEE 802.1 Q-2005 标准中指定的。 此标准是适用于 IEEE 802.1 数据中心桥接 (DCB) 接口的框架的一部分。

当网络适配器采用严格优先级的 TSA 时，它将仅根据数据包的指定 IEEE 802.1 p 优先级级别选择要传输的数据包。 因此，具有较高优先级的数据包始终在优先级较低的数据包之前传输。

微型端口驱动程序通过 \_ \_ \_ \_ \_ 在 [**ndis \_ qos \_ 功能**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_capabilities)结构的 **Flags** 成员中设置支持的 ndis qos 功能严格 驱动程序使用此结构在对 [**NdisMSetMiniportAttributes**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)的调用中注册其 NDIS QOS 和 DCB 功能。

有关优先级别的详细信息，请参阅 [IEEE 802.1 p Priority 级别](ieee-802-1p-priority-levels.md)。

**注意**  从 NDIS 6.30 开始，为 DCB 接口支持 NDIS 服务 (QoS) 的微型端口驱动程序必须播发对严格优先级 TSA 的支持。

 

 

