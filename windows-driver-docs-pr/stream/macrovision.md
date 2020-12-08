---
title: Macrovision
description: Macrovision
keywords:
- DVD 解码器微型驱动程序 WDK，版权保护
- 解码器微型驱动程序 WDK DVD，版权保护
- 版权保护 WDK DVD 解码器
- Macrovision WDK DVD 解码器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e90e415c8c5f17739ccb7653774634d281d9d1a9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96791159"
---
# <a name="macrovision"></a>Macrovision





在离开计算机之前处理视频数据的最后一个设备支持 Macrovision。 如果视频端口连接到视频卡，视频卡和 DVD 导航器/拆分器将处理所有 Macrovision 处理。 不涉及解码器。

如果解码器具有 NTSC 输出，则 Macrovision 编码和 Macrovision 符合性由解码器卡负责。 [**KS \_ COPY \_ MACROVISION**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ks_copy_macrovision)属性指示媒体上的 MACROVISION 编码级别 (级别0到 3) 。 解码器可能会使用此信息来启用或禁用针对 NTSC 输出的 Macrovision 编码。

 

