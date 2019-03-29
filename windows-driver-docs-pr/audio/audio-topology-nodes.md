---
title: 音频拓扑节点
description: 音频拓扑节点
ms.assetid: d999955b-d620-41c9-b42d-6870ce1d4b93
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: dd8984a5e2436ea38b954d148dec4949e11f1387
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56568145"
---
# <a name="audio-topology-nodes"></a>音频拓扑节点


## <span id="ddk_audio_topology_nodes_ks"></span><span id="DDK_AUDIO_TOPOLOGY_NODES_KS"></span>


WDM 音频驱动程序框架定义一组标准的音频设备的拓扑节点。 微型端口驱动程序描述设备的音频拓扑通过指定一组节点和节点之间的连接。 [SysAudio 系统驱动程序](https://msdn.microsoft.com/library/windows/hardware/ff537039#sysaudio-system-driver)使用此信息来构造它向客户端应用程序提供音频筛选器关系图。

拓扑中的每个数据路径开始或结束 pin 并通过一定数量的节点，在其中可以认为的珠子排列在沿数据路径。 唯一标识该节点中的数据路径的一个节点 ID （实质上是索引） 由标识每个节点中的数据路径。 两个 pin 实例可能有节点使用相同的 ID，但 pin 实例和节点 ID 的组合唯一地标识音频拓扑内的每个节点。

拓扑节点支持一的组节点属性。 标识属性所属的内部节点的节点 ID 的情况下，节点属性不同于 pin 属性状态。 若要获取或设置属性请求发送到特定节点，客户端指定除了目标 pin 实例之外的目标节点 ID。 Pin 的属性处理程序接收请求时，它会查看的节点 ID，并将定向到该节点的处理程序的请求。

以下列表包含更常使用的音频拓扑节点类型：

[**KSNODETYPE\_3D\_EFFECTS**](ksnodetype-3d-effects.md)

[**KSNODETYPE\_ACOUSTIC\_ECHO\_CANCEL**](ksnodetype-acoustic-echo-cancel.md)

[**KSNODETYPE\_ADC**](ksnodetype-adc.md)

[**KSNODETYPE\_AGC**](ksnodetype-agc.md)

[**KSNODETYPE\_AUDIO\_ENGINE**](ksnodetype-audio-engine.md)

[**KSNODETYPE\_AUDIO\_KEYWORDDETECTOR**](ksnodetype-audio-keyworddetector.md)

[**KSNODETYPE\_合唱团**](ksnodetype-chorus.md)

[**KSNODETYPE\_DAC**](ksnodetype-dac.md)

[**KSNODETYPE\_延迟**](ksnodetype-delay.md)

[**KSNODETYPE\_DEMUX**](ksnodetype-demux.md)

[**KSNODETYPE\_开发人员\_特定**](ksnodetype-dev-specific.md)

[**KSNODETYPE\_DMSYNTH**](ksnodetype-dmsynth.md)

[**KSNODETYPE\_DMSYNTH\_CAP**](ksnodetype-dmsynth-caps.md)

[**KSNODETYPE\_DRM\_DESCRAMBLE**](ksnodetype-drm-descramble.md)

[**KSNODETYPE\_均衡器**](ksnodetype-equalizer.md)

[**KSNODETYPE\_FM\_RX**](ksnodetype-fm-rx.md)

[**KSNODETYPE\_响度**](ksnodetype-loudness.md)

[**KSNODETYPE\_麦克风\_数组\_处理器**](ksnodetype-microphone-array-processor.md)

[**KSNODETYPE\_静音**](ksnodetype-mute.md)

[**KSNODETYPE\_MUX**](ksnodetype-mux.md)

[**KSNODETYPE\_干扰\_禁止**](ksnodetype-noise-suppress.md)

[**KSNODETYPE\_PEAKMETER**](ksnodetype-peakmeter.md)

[**KSNODETYPE\_PROLOGIC\_解码器**](ksnodetype-prologic-decoder.md)

[**KSNODETYPE\_PROLOGIC\_编码器**](ksnodetype-prologic-encoder.md)

[**KSNODETYPE\_REVERB**](ksnodetype-reverb.md)

[**KSNODETYPE\_SRC**](ksnodetype-src.md)

[**KSNODETYPE\_立体声\_增强**](ksnodetype-stereo-enhance.md)

[**KSNODETYPE\_立体声\_宽**](ksnodetype-stereo-wide.md)

[**KSNODETYPE\_总和**](ksnodetype-sum.md)

[**KSNODETYPE\_SUPERMIX**](ksnodetype-supermix.md)

[**KSNODETYPE\_SWMIDI**](ksnodetype-swmidi.md)

[**KSNODETYPE\_SWSYNTH**](ksnodetype-swsynth.md)

[**KSNODETYPE\_合成器**](ksnodetype-synthesizer.md)

[**KSNODETYPE\_TELEPHONY\_BIDI**](ksnodetype-telephony-bidi.md)

[**KSNODETYPE\_音**](ksnodetype-tone.md)

[**KSNODETYPE\_卷**](ksnodetype-volume.md)

 

 





