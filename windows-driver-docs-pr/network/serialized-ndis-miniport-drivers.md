---
title: 序列化的 NDIS 微型端口驱动程序
description: 序列化的 NDIS 微型端口驱动程序
ms.assetid: 6b9b94ad-5d5d-465a-90bc-47095f6e2b9c
keywords:
- 微型端口驱动程序 WDK 网络，类型
- NDIS 微型端口驱动程序 WDK，类型
- 序列化 NDIS 微型端口驱动程序 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c9b33ed6df22ca4c66393d682498a03fb907feff
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89214446"
---
# <a name="serialized-ndis-miniport-drivers"></a>序列化的 NDIS 微型端口驱动程序





Windows Vista 和更高版本的序列化 NDIS 微型端口驱动程序已过时。 NDIS 6.0 驱动程序不支持序列化微型端口驱动程序。 Windows Vista 仅支持 NDIS 5.1 和更早版本的驱动程序的序列化微型端口驱动程序。 与反序列化的微型端口驱动程序不同，序列化微型端口驱动程序依赖 NDIS 来序列化其自己的 *MiniportXxx* 函数的操作，并管理用于发送网络数据包的队列。

如果要编写新的微型端口驱动程序，应编写 [反序列化的驱动程序](deserialized-ndis-miniport-drivers.md)。 如果可能，还应将旧驱动程序移植到 NDIS 6.0 或更高版本。 有关将驱动程序移植到 NDIS 6.0 的详细信息，请参阅 [将 ndis 1.X 驱动程序移植到 ndis 6.0](/previous-versions/windows/hardware/network/porting-ndis-5-x-drivers-to-ndis-6-0)。

 

