---
title: KSNODETYPE \_ 回声 \_ \_ 取消
description: KSNODETYPE \_ 回声 \_ \_ 取消
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
ms.openlocfilehash: fd380124364884f5a6bdabe463200322ca6a22ef
ms.sourcegitcommit: 372464be981a39781c71049126f36891cb5d0cad
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2020
ms.locfileid: "91646009"
---
# <a name="ksnodetype_acoustic_echo_cancel"></a>KSNODETYPE \_ 回声 \_ \_ 取消


## <span id="ddk_ksnodetype_acoustic_echo_cancel_ks"></span><span id="DDK_KSNODETYPE_ACOUSTIC_ECHO_CANCEL_KS"></span>


KSNODETYPE 的 " \_ 回声" \_ \_ 取消节点表示) 控制的 AEC (声音回声取消。 AEC 节点具有两个输入流和两个输出流的连接。 一个输入/输出对用于捕获流，另一个输入/输出对用于呈现流。 捕获输出和呈现输入流具有相同的格式。 捕获输入和呈现输出流可以有不同数量的通道和不同的采样速率。 但是，在典型实现中，两个流具有相同的采样率或组合，例如 16 kHz 和 48 kHz 或 11.025 kHz 和 44.1 kHz，其中一个采样速率是另一个的整数倍。

AEC 节点应使用标头文件 Ksmedia 中的 pin Id 对其逻辑 pin 进行编号，如下表所示。

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
<td align="left"><p>接收器 pin (用于呈现流的节点输入) 。</p></td>
</tr>
<tr class="even">
<td align="left"><p>KSNODEPIN_AEC_RENDER_OUT</p></td>
<td align="left"><p>呈现流 (节点输出) 的源 pin。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>KSNODEPIN_AEC_CAPTURE_IN</p></td>
<td align="left"><p>接收器 pin (用于捕获流的节点输入) 。</p></td>
</tr>
<tr class="even">
<td align="left"><p>KSNODEPIN_AEC_CAPTURE_OUT</p></td>
<td align="left"><p>捕获流 (节点输出) 的源 pin。</p></td>
</tr>
</tbody>
</table>

 

请注意，上表中的 pin 是节点上的逻辑引脚，它们专用于指定筛选器的内部连接，而不是用于连接到其他筛选器的筛选器的外部 pin。 有关详细信息，请参阅 [**PCCONNECTION \_ 描述符**](/windows-hardware/drivers/ddi/portcls/ns-portcls-_pcconnection_descriptor)。

有关包含 AEC 节点的筛选器如何为全双工 DirectSound 应用程序提供支持的信息，请参阅 [DirectSound 捕获效果](./directsound-capture-effects.md)。

当创建包含 AEC 节点的筛选器或重置节点时，该节点最初配置为在传递模式下运行。

\_ \_ \_ 若要启用硬件加速，KSNODETYPE 的 "声音回声" 取消节点应支持以下属性：

[**KSPROPERTY \_ 音频 \_ CPU \_ 资源**](ksproperty-audio-cpu-resources.md)

[**KSPROPERTY \_ 音频 \_ 算法 \_ 实例**](ksproperty-audio-algorithm-instance.md)

[**KSPROPERTY \_ TOPOLOGYNODE \_ ENABLE**](ksproperty-topologynode-enable.md)

[**KSPROPERTY \_ TOPOLOGYNODE \_ 重置**](ksproperty-topologynode-reset.md)

KSPROPERTY \_ TOPOLOGYNODE \_ enable 属性用于启用和禁用 AEC 节点。 如果禁用，节点将在直通模式下运行;也就是说，它允许在不进行修改的情况下，将呈现和捕获流传递到节点。

KSNODETYPE 的 \_ \_ "声音回声 \_ " 取消节点还可以支持以下可选属性，以便提供其他控制和监视功能：

[**KSPROPERTY \_ AEC \_ 模式**](ksproperty-aec-mode.md)

[**KSPROPERTY \_ AEC \_ 干扰 \_ 填充 \_ 启用**](ksproperty-aec-noise-fill-enable.md)

[**KSPROPERTY \_ AEC \_ 状态**](ksproperty-aec-status.md)

 

