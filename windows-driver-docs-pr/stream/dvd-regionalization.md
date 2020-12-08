---
title: DVD 区域化
description: DVD 区域化
keywords:
- DVD 解码器微型驱动程序 WDK
- 实行 WDK DVD 解码器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0d36feb3255df8e29748b682727e4cc5108262eb
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96795355"
---
# <a name="dvd-regionalization"></a>DVD 区域化





DVD 解码器微型驱动程序不应涉及实行过程的任何部分。 流式处理体系结构的其他部分强制执行实行。 在大多数情况下，解码器微型驱动程序不实现 [**KS \_ DVDCOPY \_ 区域**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ks_dvdcopy_region) 属性。

如果解码器仅限 (按硬件或其他注意事项) 的某个区域，则它可能会响应 **KS \_ DVDCOPY \_ 区域** 属性以覆盖所有其他系统区域。 DVD 解码器微型驱动程序应正好设置一位，对应于为解码器指定的区域。 请注意，逻辑从媒体上的区域编码中 *反转* 。 例如，解码器仅适用于 USA (地区 1) 将0x01 返回到 **KS \_ DVDCOPY \_ 区域** 属性。

如果解码器提供了区域，则系统区域更改应用程序仍将起作用。 如果系统中存在其他解码器，则会更改系统区域。 请注意，Windows DVD 播放仅在系统区域和解码器区域匹配时才起作用。

 

