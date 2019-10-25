---
title: 实现特定于功能的接口
description: 实现特定于功能的接口
ms.assetid: 6a15c8b5-17ca-4658-bf52-cf9b3307e706
keywords:
- 音频微型端口驱动程序 WDK，端口类
- 微型端口驱动程序 WDK 音频，端口类
- 微型端口接口 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ab1a400576228688e10321c72a64d4273e1709ba
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833256"
---
# <a name="implementation-of-function-specific-interfaces"></a>实现特定于功能的接口


## <span id="implementation_of_function_specific_interfaces"></span><span id="IMPLEMENTATION_OF_FUNCTION_SPECIFIC_INTERFACES"></span>


典型的音频适配器卡包含音频硬件功能的集合，适配器驱动程序可以通过相应的 IMiniport*Xxx*接口集合向 WDM 音频系统公开此功能。 所有 IMiniport*Xxx*接口都继承自[IMiniport](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiport)。 每种类型的微型端口接口（wave、MIDI、拓扑等）封装了用于控制适配器卡上特定类型音频功能的微型端口驱动程序。 驱动程序还可以公开同一微型端口接口的多个实例，以表示相同（或类似）硬件函数的多个实例。

有关详细信息，请参阅[微型端口接口](miniport-interfaces.md)。

 

 




