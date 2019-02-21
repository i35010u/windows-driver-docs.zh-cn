---
title: KSNODETYPE\_合成器
description: KSNODETYPE\_合成器
ms.assetid: ef5f5068-c312-4e14-905e-c815d6e9aac2
keywords:
- KSNODETYPE_SYNTHESIZER 音频设备
topic_type:
- apiref
api_name:
- KSNODETYPE_SYNTHESIZER
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3de630d5da533fa661c0b927b3c00535cf8424bf
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543220"
---
# <a name="ksnodetypesynthesizer"></a>KSNODETYPE\_合成器


## <span id="ddk_ksnodetype_synthesizer_ks"></span><span id="DDK_KSNODETYPE_SYNTHESIZER_KS"></span>


KSNODETYPE\_合成器节点表示 MIDI 合成器。 合成器节点将作为输入 MIDI 流，并输出以下值之一：

-   批流

-   模拟音频信号

-   原始的 MIDI

DMusUART 音频示例驱动程序中 Microsoft Windows Driver Kit (WDK) 是一个微型端口驱动程序，输出原始 MIDI 到外部合成器，并包含一个合成器节点 （在其 DirectMusic pin) 的示例。

合成器节点应支持以下必需的属性：

[**KSPROPERTY\_合成器\_CAP**](https://msdn.microsoft.com/library/windows/hardware/ff537389)

[**KSPROPERTY\_合成器\_PORTPARAMETERS**](https://msdn.microsoft.com/library/windows/hardware/ff537405)

支持多个通道组的合成节点还应支持以下属性：

[**KSPROPERTY\_合成器\_CHANNELGROUPS**](https://msdn.microsoft.com/library/windows/hardware/ff537390)

如果节点不支持此属性，通道组数默认为 1。

合成器节点还可以支持以下可选[KSPROPSETID\_合成](kspropsetid-synth.md)并[KSPROPSETID\_合成器\_Dls](kspropsetid-synth-dls.md)属性：

[**KSPROPERTY\_合成器\_LATENCYCLOCK**](https://msdn.microsoft.com/library/windows/hardware/ff537402)

[**KSPROPERTY\_SYNTH\_MASTERCLOCK**](https://msdn.microsoft.com/library/windows/hardware/ff537403)

[**KSPROPERTY\_合成器\_RUNNINGSTATS**](https://msdn.microsoft.com/library/windows/hardware/ff537406)

[**KSPROPERTY\_合成器\_VOICEPRIORITY**](https://msdn.microsoft.com/library/windows/hardware/ff537407)

[**KSPROPERTY\_合成器\_卷**](https://msdn.microsoft.com/library/windows/hardware/ff537409)

[**KSPROPERTY\_合成器\_VOLUMEBOOST**](https://msdn.microsoft.com/library/windows/hardware/ff537410)

[**KSPROPERTY\_合成\_DLS\_追加**](https://msdn.microsoft.com/library/windows/hardware/ff537392)

[**KSPROPERTY\_合成\_DLS\_COMPACT**](https://msdn.microsoft.com/library/windows/hardware/ff537394)

[**KSPROPERTY\_合成\_DLS\_下载**](https://msdn.microsoft.com/library/windows/hardware/ff537396)

[**KSPROPERTY\_合成\_DLS\_卸载**](https://msdn.microsoft.com/library/windows/hardware/ff537398)

[**KSPROPERTY\_合成\_DLS\_WAVEFORMAT**](https://msdn.microsoft.com/library/windows/hardware/ff537400)

 

 





