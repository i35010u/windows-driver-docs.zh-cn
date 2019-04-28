---
title: KSNODETYPE\_声学\_ECHO\_取消
description: KSNODETYPE\_声学\_ECHO\_取消
ms.assetid: 5f70b9ad-d569-404a-bf6d-01be689e2d56
keywords:
- KSNODETYPE_ACOUSTIC_ECHO_CANCEL 音频设备
topic_type:
- apiref
api_name:
- KSNODETYPE_ACOUSTIC_ECHO_CANCEL
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: a39a0dd120a647f9c6329b1e30b31a7d329e5e34
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63333288"
---
# <a name="ksnodetypeacousticechocancel"></a>KSNODETYPE\_声学\_ECHO\_取消


## <span id="ddk_ksnodetype_acoustic_echo_cancel_ks"></span><span id="DDK_KSNODETYPE_ACOUSTIC_ECHO_CANCEL_KS"></span>


KSNODETYPE\_声学\_ECHO\_取消节点表示的 AEC （回声抵消） 控件。 AEC 节点具有两个输入流的连接和两个输出流。 一个输入/输出对用于捕获流和其他输入/输出对用于呈现流。 捕获输出和呈现输入流具有相同的格式。 捕获输入和呈现输出流可以具有不同数目的通道和不同抽样率。 但是，在典型的实现中，两个流具有相同的采样率或组合，例如 16 kHz 和 48khz 或 11.025 kHz 和 44.1 kHz，速率中的一个示例是一个整数，另一个的多个。

AEC 节点应号其逻辑插针，具有 pin Id 标头文件 Ksmedia.h，从下表中所示。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Pin ID 参数</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>KSNODEPIN_AEC_RENDER_IN</p></td>
<td align="left"><p>为呈现的流式传输接收器 pin （节点输入）。</p></td>
</tr>
<tr class="even">
<td align="left"><p>KSNODEPIN_AEC_RENDER_OUT</p></td>
<td align="left"><p>源 pin 码 （节点输出） 以进行呈现流。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>KSNODEPIN_AEC_CAPTURE_IN</p></td>
<td align="left"><p>接收器为捕获的流的 pin （节点输入）。</p></td>
</tr>
<tr class="even">
<td align="left"><p>KSNODEPIN_AEC_CAPTURE_OUT</p></td>
<td align="left"><p>为捕获的流的源 pin （节点输出）。</p></td>
</tr>
</tbody>
</table>

 

请注意上, 表中的针逻辑引脚的节点上，这些信息仅用于指定连接到筛选器内部，而不是外部的插针上筛选器，用于连接到其他筛选器。 有关详细信息，请参阅[ **PCCONNECTION\_描述符**](https://msdn.microsoft.com/library/windows/hardware/ff537688)。

有关如何筛选器包含 AEC 节点可以为全双工 DirectSound 应用程序提供支持的信息，请参阅[DirectSound 捕获效果](https://msdn.microsoft.com/library/windows/hardware/ff536327)。

当创建筛选器包含 AEC 节点或节点重置时，节点最初配置为在直通模式下操作。

KSNODETYPE\_声学\_ECHO\_取消节点应以启用硬件加速支持以下属性：

[**KSPROPERTY\_AUDIO\_CPU\_RESOURCES**](ksproperty-audio-cpu-resources.md)

[**KSPROPERTY\_音频\_算法\_实例**](ksproperty-audio-algorithm-instance.md)

[**KSPROPERTY\_TOPOLOGYNODE\_启用**](ksproperty-topologynode-enable.md)

[**KSPROPERTY\_TOPOLOGYNODE\_重置**](ksproperty-topologynode-reset.md)

KSPROPERTY\_TOPOLOGYNODE\_启用属性用于启用和禁用 AEC 节点。 禁用时，该节点的同类直通模式;即，它允许通过无需修改节点的呈现和捕获流。

KSNODETYPE\_声学\_ECHO\_取消节点还可以以提供更多控制和监视功能支持以下可选属性：

[**KSPROPERTY\_AEC\_模式**](ksproperty-aec-mode.md)

[**KSPROPERTY\_AEC\_NOISE\_FILL\_ENABLE**](ksproperty-aec-noise-fill-enable.md)

[**KSPROPERTY\_AEC\_状态**](ksproperty-aec-status.md)

 

 





