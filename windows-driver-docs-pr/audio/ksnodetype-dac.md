---
title: KSNODETYPE\_DAC
description: KSNODETYPE\_DAC
ms.assetid: 70b30425-cffc-49e1-aa8b-8f5734bd196e
keywords:
- KSNODETYPE_DAC 音频设备
topic_type:
- apiref
api_name:
- KSNODETYPE_DAC
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 38cf31e47ab2f9c0a6583a25daee3d8a320d1fd9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63333256"
---
# <a name="ksnodetypedac"></a>KSNODETYPE\_DAC


## <span id="ddk_ksnodetype_dac_ks"></span><span id="DDK_KSNODETYPE_DAC_KS"></span>


KSNODETYPE\_DAC 节点表示的数字模拟转换器 (DAC)。 DAC 节点都有一个输入的流和一个输出流。

一个很好的一般规则是音频驱动程序应公开其拓扑中的只有一个 DAC 节点。 DirectSound 假设驱动程序的拓扑包含单个 DAC 节点，因为它扬声器配置属性将请求发送到其发现的第一个 DAC 节点，但不适用于任何其他。 事实上，拓扑可以安全地包含多个 DAC 的节点，但仅，如果所有 DAC 节点都表示相同的物理控制。 在这种情况下，DAC 节点中的任何一个上设置属性具有 DAC 的所有节点上设置相同的属性的影响。 一些音频驱动程序可能需要使用多个 DAC 节点我解决 Windows 中的问题 / 98，Windows 2000 和 Windows XP:如果微型端口驱动程序提供了多个批呈现 pin 工厂，并且具有混合了从这些引脚一起通过源 DAC 节点和节点流的拓扑，wdmaud.drv （mixer 行驱动程序） 将错误地报告的单独的批音量控件为每个 pin 工厂。 它应生成仅单个批音量控件。 若要解决此问题，解决解决方案是将 DAC 节点插入到每个 pin 工厂中的数据路径。

KSNODETYPE\_DAC 的节点可以支持以下可选属性：

[**KSPROPERTY\_音频\_通道\_配置**](ksproperty-audio-channel-config.md)

[**KSPROPERTY\_AUDIO\_DYNAMIC\_SAMPLING\_RATE**](ksproperty-audio-dynamic-sampling-rate.md)

[**KSPROPERTY\_AUDIO\_SAMPLING\_RATE**](ksproperty-audio-sampling-rate.md)

[**KSPROPERTY\_音频\_立体声\_演讲者\_GEOMETRY**](ksproperty-audio-stereo-speaker-geometry.md)

 

 





