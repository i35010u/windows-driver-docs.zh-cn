---
title: 指示 RSS 接收数据
description: 指示 RSS 接收数据
ms.assetid: 8d040d7d-3a8a-4d81-8508-8de225e000ab
keywords:
- 接收方缩放的 WDK 网络，，该值指示接收数据
- RSS WDK 网络，该值指示接收数据
- 指示接收数据 WDK RSS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8178350f17c802aacdc5e274e99dad311a10c8ec
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523163"
---
# <a name="indicating-rss-receive-data"></a>指示 RSS 接收数据





微型端口驱动程序通过调用指示接收到的数据[ **NdisMIndicateReceiveNetBufferLists** ](https://msdn.microsoft.com/library/windows/hardware/ff563598)函数从其[ *MiniportInterruptDPC*](https://msdn.microsoft.com/library/windows/hardware/ff559398)函数。

NIC 已成功计算 RSS 哈希值后，驱动程序应存储哈希类型，哈希函数，并且哈希值中的[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388)结构下列宏：

[**NET\_BUFFER\_LIST\_SET\_HASH\_TYPE**](https://msdn.microsoft.com/library/windows/hardware/ff568409)

[**NET\_BUFFER\_LIST\_SET\_HASH\_FUNCTION**](https://msdn.microsoft.com/library/windows/hardware/ff568408)

[**NET\_BUFFER\_LIST\_SET\_HASH\_VALUE**](https://msdn.microsoft.com/library/windows/hardware/ff568410)

哈希类型可标识应通过计算哈希所接收数据包的区域。 有关哈希类型的详细信息，请参阅[RSS 哈希算法类型](rss-hashing-types.md)。 哈希函数标识用于计算哈希值的函数。 有关哈希函数的详细信息，请参阅[RSS 哈希函数](rss-hashing-functions.md)。 协议驱动程序选择的哈希类型和函数在初始化时。 有关详细信息，请参阅[RSS 配置](rss-configuration.md)。

如果 NIC 无法识别的区域的数据包的哈希类型指定，则不应任何哈希计算或缩放。 在这种情况下，微型端口驱动程序或 NIC 应该接收到的数据为分配的默认 CPU。

如果 NIC 用尽了接收缓冲区，每个缓冲区必须返回原始接收时，就立即 DPC 返回。 微型端口驱动程序可以指示接收到的数据的状态为 NDIS\_状态\_资源。 在这种情况下，基础驱动程序必须经过复制缓冲区描述符和立即释放原始的所有权的慢速路径。

有关接收网络数据的详细信息，请参阅[接收网络数据](receiving-network-data.md)。

 

 





