---
title: 严格优先级算法
description: 严格优先级算法
ms.assetid: 7C7A34CA-673C-4EFC-970D-08458AA83EAD
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 99839b374b6241c564493c5caf8ff44f6c2cd49b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63366369"
---
# <a name="strict-priority-algorithm"></a>严格优先级算法


严格的优先级是 IEEE 802.1Q 中指定的传输选择算法 (TSA)-2005 标准。 此标准是 framework 的 IEEE 802.1 数据中心桥接 (DCB) 接口的一部分。

网络适配器采用严格的优先级 TSA，它会选择数据包，为完全根据数据包的传输指定的 IEEE 802.1p 优先级级别。 因此，具有更高的优先级级别的数据包始终传输之前的数据包，其中较低优先级别。

微型端口驱动程序指定它对严格的优先级 TSA 的支持通过设置 NDIS\_QOS\_功能\_STRICT\_TSA\_中支持**标志**成员[ **NDIS\_QOS\_功能**](https://msdn.microsoft.com/library/windows/hardware/hh451629)结构。 驱动程序使用此结构在调用注册它 NDIS QoS 和 DCB 的功能[ **NdisMSetMiniportAttributes**](https://msdn.microsoft.com/library/windows/hardware/ff563672)。

有关优先级级别的详细信息，请参阅[IEEE 802.1p 优先级](ieee-802-1p-priority-levels.md)。

**请注意**  开头 NDIS 6.30 支持 DCB 的 NDIS 服务质量 (QoS) 的微型端口驱动程序接口必须播发对严格的优先级 TSA 的支持。

 

 

 





