---
title: KSNODETYPE \_ DAC
description: KSNODETYPE \_ DAC
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
ms.openlocfilehash: 3679defb69e397204ece8f9018dcce481e8d3266
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96799163"
---
# <a name="ksnodetype_dac"></a>KSNODETYPE \_ DAC


## <span id="ddk_ksnodetype_dac_ks"></span><span id="DDK_KSNODETYPE_DAC_KS"></span>


KSNODETYPE \_ dac 节点表示 (dac) 的数字到模拟转换器。 DAC 节点有一个输入流和一个输出流。

好的一般规则是，音频驱动程序在其拓扑中只应公开一个 DAC 节点。 由于 DirectSound 假定驱动程序的拓扑仅包含一个 DAC 节点，因此它会将扬声器配置属性请求发送到它发现的第一个 DAC 节点，而不是发送到任何其他节点。 事实上，拓扑可以安全地包含多个 DAC 节点，但前提是所有 DAC 节点都表示相同的物理控件。 在这种情况下，在任何一个 DAC 节点上设置属性都具有在所有 DAC 节点上设置相同属性的效果。 某些音频驱动程序可能需要使用多个 DAC 节点来解决 Windows Me/98 中的问题，Windows 2000 和 Windows XP：如果微型端口驱动程序提供了多个波形呈现端口工厂，并且具有一个拓扑，该拓扑通过馈送 DAC 节点的 SUM 节点 wdmaud，将流与这些 pin 组合在一起，) 会错误地为每个 pin 工厂报告 (单独的波形音量控件。 它应仅生成一个波形音量控件。 若要解决此问题，一种解决方法是将 DAC 节点插入到每个 pin 工厂的数据路径中。

KSNODETYPE \_ DAC 节点可以支持以下可选属性：

[**KSPROPERTY \_ 音频 \_ 通道 \_ 配置**](ksproperty-audio-channel-config.md)

[**KSPROPERTY \_ 音频 \_ 动态 \_ 采样 \_ 速率**](ksproperty-audio-dynamic-sampling-rate.md)

[**KSPROPERTY \_ 音频 \_ 采样 \_ 率**](ksproperty-audio-sampling-rate.md)

[**KSPROPERTY \_ 音频 \_ 立体声 \_ 扬声器 \_ 几何**](ksproperty-audio-stereo-speaker-geometry.md)

 

 





