---
title: 严格优先级算法
description: 严格优先级算法
ms.assetid: 7C7A34CA-673C-4EFC-970D-08458AA83EAD
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c7f777a209c2e5ccb123c72d5a9a0f71e07a59ef
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841814"
---
# <a name="strict-priority-algorithm"></a>严格优先级算法


严格优先级是在 IEEE 802.1 Q-2005 标准中指定的传输选择算法（TSA）。 此标准是适用于 IEEE 802.1 数据中心桥接（DCB）接口的框架的一部分。

当网络适配器采用严格优先级的 TSA 时，它将仅根据数据包的指定 IEEE 802.1 p 优先级级别选择要传输的数据包。 因此，具有较高优先级的数据包始终在优先级较低的数据包之前传输。

微型端口驱动程序通过将 ndis\_QOS\_功能设置为对 strict 优先级 TSA 的支持，\_\_在 [**ndis\_qos\_功能的 FLAGS 成员中支持**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_capabilities)结构。 驱动程序使用此结构在对[**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)的调用中注册其 NDIS QOS 和 DCB 功能。

有关优先级别的详细信息，请参阅[IEEE 802.1 p Priority 级别](ieee-802-1p-priority-levels.md)。

**注意**  从 NDIS 6.30 开始，为 DCB 接口支持 NDIS 服务质量（QoS）的微型端口驱动程序必须播发对严格优先级 TSA 的支持。

 

 

 





