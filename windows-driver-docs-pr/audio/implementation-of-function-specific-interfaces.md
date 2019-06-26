---
title: 实现特定于功能的接口
description: 实现特定于功能的接口
ms.assetid: 6a15c8b5-17ca-4658-bf52-cf9b3307e706
keywords:
- 音频的微型端口驱动程序 WDK，端口类
- 微型端口驱动程序 WDK 音频，端口类
- 微型端口接口 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4c646dc9a6704081994cdbc3fa3226dfdcd4b7fb
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67359940"
---
# <a name="implementation-of-function-specific-interfaces"></a>实现特定于功能的接口


## <span id="implementation_of_function_specific_interfaces"></span><span id="IMPLEMENTATION_OF_FUNCTION_SPECIFIC_INTERFACES"></span>


典型的音频适配器卡包含的音频硬件功能，适配器驱动程序可以公开到 WDM 音频系统通过 IMiniport 的相应集合集合*Xxx*接口。 所有 IMiniport*Xxx*接口继承自[IMiniport](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iminiport)。 每个的微型端口接口-批，MIDI，拓扑中，键入并因此 – 封装用于控制特定类型的适配器卡上的音频函数的微型端口驱动程序。 驱动程序还可以公开相同的微型端口接口，来表示相同 （或类似） 的硬件功能的多个实例的多个实例。

有关详细信息，请参阅[微型端口接口](miniport-interfaces.md)。

 

 




