---
title: 音频拓扑节点
description: 音频拓扑节点
ms.assetid: d999955b-d620-41c9-b42d-6870ce1d4b93
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: dcd760c6f4ccd62e400cf8d5d5a8c7fe77d31ae4
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89208246"
---
# <a name="audio-topology-nodes"></a>音频拓扑节点


## <span id="ddk_audio_topology_nodes_ks"></span><span id="DDK_AUDIO_TOPOLOGY_NODES_KS"></span>


WDM 音频驱动程序框架定义音频设备的一组标准拓扑节点。 微型端口驱动程序通过指定一组节点以及节点之间的连接来描述设备的音频拓扑。 [SysAudio 系统驱动程序](./kernel-mode-wdm-audio-components.md#sysaudio-system-driver)使用此信息来构造它提供给客户端应用程序的音频筛选器图形。

拓扑中的每个数据路径都从一个 pin 开始或结束，并传递一些节点，这些节点可被视为沿数据路径的 beads 排列在。 数据路径中的每个节点都由节点 ID 标识， (本质上是唯一标识数据路径中该节点的索引) 。 两个 pin 实例可以具有具有相同 ID 的节点，但 pin 实例和节点 ID 的组合可以唯一地标识音频拓扑中的每个节点。

拓扑节点支持一组节点属性。 节点属性与 pin 属性的不同之处在于包含标识属性所属的内部节点的节点 ID。 若要将获取或设置属性请求发送到特定节点，客户端除了指定目标 pin 实例外，还指定目标节点 ID。 当 pin 的属性处理程序收到请求时，它会查看节点 ID，并将请求定向到该节点的处理程序。

以下列表包含更常用的音频拓扑节点类型：

[**KSNODETYPE \_ 三维 \_ 效果**](ksnodetype-3d-effects.md)

[**KSNODETYPE \_ 回声 \_ \_ 取消**](ksnodetype-acoustic-echo-cancel.md)

[**KSNODETYPE \_ ADC**](ksnodetype-adc.md)

[**KSNODETYPE \_ AGC**](ksnodetype-agc.md)

[**KSNODETYPE \_ 音频 \_ 引擎**](ksnodetype-audio-engine.md)

[**KSNODETYPE \_ 音频 \_ KEYWORDDETECTOR**](ksnodetype-audio-keyworddetector.md)

[**KSNODETYPE \_ CHORUS**](ksnodetype-chorus.md)

[**KSNODETYPE \_ DAC**](ksnodetype-dac.md)

[**KSNODETYPE \_ 延迟**](ksnodetype-delay.md)

[**KSNODETYPE \_ 多路分解器**](ksnodetype-demux.md)

[**KSNODETYPE \_ 开发人员 \_ 特定**](ksnodetype-dev-specific.md)

[**KSNODETYPE \_ DMSYNTH**](ksnodetype-dmsynth.md)

[**KSNODETYPE \_ DMSYNTH \_ CAP**](ksnodetype-dmsynth-caps.md)

[**KSNODETYPE \_ DRM \_ DESCRAMBLE**](ksnodetype-drm-descramble.md)

[**KSNODETYPE \_ 均衡器**](ksnodetype-equalizer.md)

[**KSNODETYPE \_ FM \_ RX**](ksnodetype-fm-rx.md)

[**KSNODETYPE \_ 响度**](ksnodetype-loudness.md)

[**KSNODETYPE \_ 麦克风 \_ 阵列 \_ 处理器**](ksnodetype-microphone-array-processor.md)

[**KSNODETYPE \_ 静音**](ksnodetype-mute.md)

[**KSNODETYPE \_ MUX**](ksnodetype-mux.md)

[**KSNODETYPE \_ 干扰 \_**](ksnodetype-noise-suppress.md)

[**KSNODETYPE \_ PEAKMETER**](ksnodetype-peakmeter.md)

[**KSNODETYPE \_ PROLOGIC \_ 解码器**](ksnodetype-prologic-decoder.md)

[**KSNODETYPE \_ PROLOGIC \_ 编码器**](ksnodetype-prologic-encoder.md)

[**KSNODETYPE \_ 回音**](ksnodetype-reverb.md)

[**KSNODETYPE \_ SRC**](ksnodetype-src.md)

[**KSNODETYPE \_ 立体声 \_ 增强**](ksnodetype-stereo-enhance.md)

[**KSNODETYPE \_ 立体声 \_**](ksnodetype-stereo-wide.md)

[**KSNODETYPE \_ SUM**](ksnodetype-sum.md)

[**KSNODETYPE \_ SUPERMIX**](ksnodetype-supermix.md)

[**KSNODETYPE \_ SWMIDI**](ksnodetype-swmidi.md)

[**KSNODETYPE \_ SWSYNTH**](ksnodetype-swsynth.md)

[**KSNODETYPE \_ 合成器**](ksnodetype-synthesizer.md)

[**KSNODETYPE \_ 电话 \_ 双向**](ksnodetype-telephony-bidi.md)

[**KSNODETYPE \_ 音**](ksnodetype-tone.md)

[**KSNODETYPE \_ 卷**](ksnodetype-volume.md)

 

