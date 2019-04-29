---
title: Macrovision
description: Macrovision
ms.assetid: 62bd8d8a-3e58-4bca-a32d-ff792180afbe
keywords:
- DVD 解码器微型驱动程序 WDK，版权保护
- 解码器微型驱动程序 WDK DVD，版权保护
- 版权保护的 WDK DVD 解码器
- Macrovision WDK DVD 解码器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9ce764548348c594cf31379a3a5d804ffc02add2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391388"
---
# <a name="macrovision"></a>Macrovision





Macrovision 受离开计算机前处理的视频数据的最后一个设备。 对于视频端口连接到的视频卡时，视频卡和 DVD 导航器/拆分器处理所有 Macrovision 处理。 解码器不涉及。

如果解码器有 NTSC 输出、 Macrovision 编码和 Macrovision 法规遵从性是解码器卡的责任。 [ **KS\_副本\_MACROVISION** ](https://msdn.microsoft.com/library/windows/hardware/ff567316)属性指示的 Macrovision 编码媒体 （级别 0 到 3） 上的级别。 解码器可能会使用此信息来启用或禁用 Macrovision NTSC 输出编码。

 

 




