---
title: 序列化的 NDIS 微型端口驱动程序
description: 序列化的 NDIS 微型端口驱动程序
ms.assetid: 6b9b94ad-5d5d-465a-90bc-47095f6e2b9c
keywords:
- 微型端口驱动程序 WDK 网络类型
- NDIS 微型端口驱动程序 WDK，类型
- 序列化的 NDIS 微型端口驱动程序 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bb28d4660b446527ffafd3b1ecbdca5ecf7e1edb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63346757"
---
# <a name="serialized-ndis-miniport-drivers"></a>序列化的 NDIS 微型端口驱动程序





序列化的 NDIS 微型端口驱动程序是适用于 Windows Vista 和更高版本已过时。 NDIS 6.0 驱动程序不支持序列化的微型端口驱动程序。 Windows Vista 支持仅为 NDIS 5.1 及更早的驱动程序序列化微型端口驱动程序。 与反序列化的微型端口驱动程序不同序列化的微型端口驱动程序依赖于要序列化的操作的 NDIS *MiniportXxx*函数以及管理用于发送数据的网络数据包的队列。

如果你正在编写新的微型端口驱动程序，您应编写[反序列化的驱动程序](deserialized-ndis-miniport-drivers.md)。 如果可能，你还应端口旧驱动程序到 NDIS 6.0 或更高版本。 有关移植到 NDIS 6.0 的驱动程序的详细信息，请参阅[到 NDIS 6.0 移植 NDIS 5.x 驱动程序](https://docs.microsoft.com/previous-versions/windows/hardware/network/porting-ndis-5-x-drivers-to-ndis-6-0)。

 

 





