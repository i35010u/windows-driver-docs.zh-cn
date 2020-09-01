---
title: KSNODETYPE \_ 合成器
description: KSNODETYPE \_ 合成器
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
ms.openlocfilehash: 2b41765c75622f3e57bf68558490ff737db38d5a
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89206999"
---
# <a name="ksnodetype_synthesizer"></a>KSNODETYPE \_ 合成器


## <span id="ddk_ksnodetype_synthesizer_ks"></span><span id="DDK_KSNODETYPE_SYNTHESIZER_KS"></span>


KSNODETYPE \_ 合成器节点表示 MIDI 合成器。 合成节点采用 MIDI 流作为输入，并输出以下内容之一：

-   波形流

-   模拟音频信号

-   原始 MIDI

 (WDK) 的 Microsoft Windows 驱动程序工具包中的 DMusUART 音频示例驱动程序是一个微型端口驱动程序示例，该驱动程序将原始 MIDI 输出到外部合成器并在其 DirectMusic pin) 上包含合成节点 (。

合成节点应支持以下必需属性：

[**KSPROPERTY \_ 合成 \_ CAP**](/previous-versions/ff537389(v=vs.85))

[**KSPROPERTY \_ 合成 \_ PORTPARAMETERS**](/previous-versions/ff537405(v=vs.85))

支持多个通道组的合成节点还应支持以下属性：

[**KSPROPERTY \_ 合成 \_ CHANNELGROUPS**](/previous-versions/ff537390(v=vs.85))

如果该节点不支持此属性，则通道组的数量默认为1。

合成节点还可以支持以下可选的 [KSPROPSETID \_ 合成](kspropsetid-synth.md) 和 [KSPROPSETID \_ 合成 \_ Dls](kspropsetid-synth-dls.md) 属性：

[**KSPROPERTY \_ 合成 \_ LATENCYCLOCK**](/previous-versions/ff537402(v=vs.85))

[**KSPROPERTY \_ 合成 \_ MASTERCLOCK**](/previous-versions/ff537403(v=vs.85))

[**KSPROPERTY \_ 合成 \_ RUNNINGSTATS**](/previous-versions/ff537406(v=vs.85))

[**KSPROPERTY \_ 合成 \_ VOICEPRIORITY**](/previous-versions/ff537407(v=vs.85))

[**KSPROPERTY \_ 合成 \_ 音量**](/previous-versions/ff537409(v=vs.85))

[**KSPROPERTY \_ 合成 \_ VOLUMEBOOST**](/previous-versions/ff537410(v=vs.85))

[**KSPROPERTY \_ 合成 \_ DL \_ APPEND**](/previous-versions/ff537392(v=vs.85))

[**KSPROPERTY \_ 合成 \_ DL \_ COMPACT**](/previous-versions/ff537394(v=vs.85))

[**KSPROPERTY \_ 合成 \_ DL \_ 下载**](/previous-versions/ff537396(v=vs.85))

[**KSPROPERTY \_ 合成 \_ DL \_ 卸载**](/previous-versions/ff537398(v=vs.85))

[**KSPROPERTY \_ 合成 \_ DL \_ WAVEFORMAT**](/previous-versions/ff537400(v=vs.85))

 

