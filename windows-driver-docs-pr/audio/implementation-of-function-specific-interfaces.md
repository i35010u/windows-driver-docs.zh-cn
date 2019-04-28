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
ms.openlocfilehash: 890d971a24494f14a2598046ae2b60221d6fc705
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63333552"
---
# <a name="implementation-of-function-specific-interfaces"></a>实现特定于功能的接口


## <span id="implementation_of_function_specific_interfaces"></span><span id="IMPLEMENTATION_OF_FUNCTION_SPECIFIC_INTERFACES"></span>


典型的音频适配器卡包含的音频硬件功能，适配器驱动程序可以公开到 WDM 音频系统通过 IMiniport 的相应集合集合*Xxx*接口。 所有 IMiniport*Xxx*接口继承自[IMiniport](https://msdn.microsoft.com/library/windows/hardware/ff536698)。 每个的微型端口接口-批，MIDI，拓扑中，键入并因此 – 封装用于控制特定类型的适配器卡上的音频函数的微型端口驱动程序。 驱动程序还可以公开相同的微型端口接口，来表示相同 （或类似） 的硬件功能的多个实例的多个实例。

有关详细信息，请参阅[微型端口接口](miniport-interfaces.md)。

 

 




