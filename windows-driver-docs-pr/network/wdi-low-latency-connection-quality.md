---
title: WDI 低延迟连接质量
description: 本部分介绍如何维护使用 WDI 中的低延迟连接质量
ms.assetid: 194A26DA-A138-4967-9A09-5843A38007E9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b5e0e06a362fbde672c908d387a61e9e69dbb694
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63385405"
---
# <a name="wdi-low-latency-connection-quality"></a>WDI 低延迟连接质量


如果需要低延迟数据流量 （例如，VoIP 应用程序） 在系统上运行的应用程序，可以将端口配置为较低的延迟模式下操作。 在此模式下的操作，该驱动程序应修改任何行为将导致离开的低延迟模式下配置的端口的通道 （如扫描或更高 AP 漫游)。 它还应遵循的指定的指南[NDIS\_状态\_WDI\_指示\_链接\_状态\_更改](https://msdn.microsoft.com/library/windows/hardware/dn925638)指示。 主机提供[ **WDI\_TLV\_低\_延迟\_连接\_质量\_参数**](https://msdn.microsoft.com/library/windows/hardware/dn897843)的端口在此模式下时，应使用。 这将指定该端口应为关闭通道和连接启动较低的延迟漫游之前必须在向下的最小链接质量值的最长时间 (包括发送[NDIS\_状态\_WDI\_指示\_漫游\_需执行](https://msdn.microsoft.com/library/windows/hardware/dn925648))。

扫描主机提供 （有不同的值为主动和被动通道） 的最大通道停留时间和适配器应不超过最长时间。 主机还限制不必要的扫描。 但是，适配器可以限制扫描进一步 if [ **WDI\_扫描\_触发器**](https://msdn.microsoft.com/library/windows/hardware/dn926114)是**WDI\_扫描\_触发器\_背景**或**WDI\_扫描\_触发器\_漫游**。 如果适配器在此模式下执行其自己的扫描，则建议，它包含在寻找 （除非它是从睡眠状态恢复后） 来减少的通道上的停留时间的 SSID。 此外，它应避免扫描单个通道关闭扫描中的多个通道，以便它在整体关闭通道时间限制之内。

主机认为[NDIS\_状态\_WDI\_指示\_漫游\_需执行](https://msdn.microsoft.com/library/windows/hardware/dn925648)漫游，因此在此模式下，适配器应该从适配器的强请求谨慎发送这种指示是何种频率。 如果适配器执行其自身漫游/AP 选择决策，它必须采用适当的机制 （如邻居报表或 PMKIDs） 来查找和选择/排名 APs。

若要优化关联进程，适配器应使用缓存的 BSS 条目 TSF 计时器同步在加入期间在可能的情况。 缓存的条目应足以有关 TSF 计时器同步，这是最新的大部分时间，因为已获取了从最新的探测请求。 TSF 同步可以进行更高版本，即使驱动程序决定选择不具有最新的缓存的探测响应的接入点。 该驱动程序可以禁用 Wi-fi 节能，直到收到的下一步的信号，在 100 毫秒内，通常会出现。

在多渠道并发模式下操作时，建议，适配器使用 ECSA 或其他机制，可启用无缝/无抖动体验执行多路复用通道时。

 

 





