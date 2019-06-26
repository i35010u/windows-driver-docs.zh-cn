---
title: DVD 区域化
description: DVD 区域化
ms.assetid: 931441c8-9521-43c9-86f1-dbf75d36e190
keywords:
- DVD 解码器微型驱动程序 WDK
- 区域化 WDK DVD 解码器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4bf9536cf9620b571f18683090d6c3f48d70fe5a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384147"
---
# <a name="dvd-regionalization"></a>DVD 区域化





DVD 解码器微型驱动程序不应为参与区域化过程的任何部分。 流式处理体系结构的其他部分强制执行之前实行。 在大多数情况下，解码器微型驱动程序不实现[ **KS\_DVDCOPY\_区域**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-_ks_dvdcopy_region)属性。

如果解码器被限制为特定的区域 （由硬件或其他考虑因素），则它可能会响应**KS\_DVDCOPY\_区域**属性重写所有其他系统区域。 DVD 解码器微型驱动程序应设置完全与解码器被指定为该区域对应一位。 请注意，逻辑*反转*从媒体上的地区编码。 例如，用于处理仅在区域 1 （美国） 的解码器返回到 0x01 **KS\_DVDCOPY\_区域**属性。

如果解码器提供了一个区域，系统区域将更改应用程序仍函数。 在系统中有其他解码器的情况下，它会更改系统区域。 请注意 Windows DVD 播放仅函数是否系统区域与解码器区域相匹配。

 

 




