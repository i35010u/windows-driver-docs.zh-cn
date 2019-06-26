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
ms.openlocfilehash: 6901d4a57865c3f073805affe790bb0a40ea769a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67359010"
---
# <a name="ksnodetypesynthesizer"></a>KSNODETYPE\_合成器


## <span id="ddk_ksnodetype_synthesizer_ks"></span><span id="DDK_KSNODETYPE_SYNTHESIZER_KS"></span>


KSNODETYPE\_合成器节点表示 MIDI 合成器。 合成器节点将作为输入 MIDI 流，并输出以下值之一：

-   批流

-   模拟音频信号

-   原始的 MIDI

DMusUART 音频示例驱动程序中 Microsoft Windows Driver Kit (WDK) 是一个微型端口驱动程序，输出原始 MIDI 到外部合成器，并包含一个合成器节点 （在其 DirectMusic pin) 的示例。

合成器节点应支持以下必需的属性：

[**KSPROPERTY\_合成器\_CAP**](https://docs.microsoft.com/previous-versions/ff537389(v=vs.85))

[**KSPROPERTY\_合成器\_PORTPARAMETERS**](https://docs.microsoft.com/previous-versions/ff537405(v=vs.85))

支持多个通道组的合成节点还应支持以下属性：

[**KSPROPERTY\_合成器\_CHANNELGROUPS**](https://docs.microsoft.com/previous-versions/ff537390(v=vs.85))

如果节点不支持此属性，通道组数默认为 1。

合成器节点还可以支持以下可选[KSPROPSETID\_合成](kspropsetid-synth.md)并[KSPROPSETID\_合成器\_Dls](kspropsetid-synth-dls.md)属性：

[**KSPROPERTY\_合成器\_LATENCYCLOCK**](https://docs.microsoft.com/previous-versions/ff537402(v=vs.85))

[**KSPROPERTY\_SYNTH\_MASTERCLOCK**](https://docs.microsoft.com/previous-versions/ff537403(v=vs.85))

[**KSPROPERTY\_合成器\_RUNNINGSTATS**](https://docs.microsoft.com/previous-versions/ff537406(v=vs.85))

[**KSPROPERTY\_合成器\_VOICEPRIORITY**](https://docs.microsoft.com/previous-versions/ff537407(v=vs.85))

[**KSPROPERTY\_合成器\_卷**](https://docs.microsoft.com/previous-versions/ff537409(v=vs.85))

[**KSPROPERTY\_合成器\_VOLUMEBOOST**](https://docs.microsoft.com/previous-versions/ff537410(v=vs.85))

[**KSPROPERTY\_合成\_DLS\_追加**](https://docs.microsoft.com/previous-versions/ff537392(v=vs.85))

[**KSPROPERTY\_合成\_DLS\_COMPACT**](https://docs.microsoft.com/previous-versions/ff537394(v=vs.85))

[**KSPROPERTY\_合成\_DLS\_下载**](https://docs.microsoft.com/previous-versions/ff537396(v=vs.85))

[**KSPROPERTY\_合成\_DLS\_卸载**](https://docs.microsoft.com/previous-versions/ff537398(v=vs.85))

[**KSPROPERTY\_合成\_DLS\_WAVEFORMAT**](https://docs.microsoft.com/previous-versions/ff537400(v=vs.85))

 

 





