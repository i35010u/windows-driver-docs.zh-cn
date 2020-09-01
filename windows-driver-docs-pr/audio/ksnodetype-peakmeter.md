---
title: KSNODETYPE \_ PEAKMETER
description: KSNODETYPE \_ PEAKMETER
ms.assetid: 11c886eb-dd63-44dd-9bca-dd19a8dd6948
keywords:
- KSNODETYPE_PEAKMETER 音频设备
topic_type:
- apiref
api_name:
- KSNODETYPE_PEAKMETER
api_type:
- NA
ms.date: 04/21/2020
ms.localizationpriority: medium
ms.openlocfilehash: f34d86c0fb4c63847fadf3426257303a687d8f3a
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89207003"
---
# <a name="ksnodetype_peakmeter"></a>KSNODETYPE \_ PEAKMETER

## <span id="ddk_ksnodetype_peakmeter_ks"></span><span id="DDK_KSNODETYPE_PEAKMETER_KS"></span>

**KSNODETYPE \_ PEAKMETER**节点表示硬件 PEAKMETER。 KS peakmeter 节点有一个输入插针和一个输出插针，这两个 pin 共享相同的数据格式。

当 peakmeter 重置为零时，KS peakmeter 内部记录音频信号的最大值。 在 IOCTL KS 属性请求之后，peakmeter 会自动将自身重置为零， \_ \_ 以获取 [**KSPROPERTY \_ 音频 \_ PEAKMETER2**](ksproperty-audio-peakmeter2.md) 属性。

Peakmeter 需要硬件支持。 软件 peakmeter 是不可行的，这是因为适配器驱动程序无法访问出现在与播放通道混合的行输入、麦克风或其他输入上的信号。

Microsoft 建议使 peakmeter 节点成为流在筛选器中传递的最终节点。 在呈现流上，音频适配器通常在主输出 [**KSNODETYPE \_ 静音**](ksnodetype-mute.md) 节点或 [**KSNODETYPE \_ 卷**](ksnodetype-volume.md) 节点之后连接 peakmeter 节点。 同样的方法适用于捕获流或筛选器合并了 peakmeter 节点的任何其他流。

音频适配器应将 peakmeter 节点命名为 KSAUDFNAME \_ peakmeter。

Peakmeter 节点应为属性标志提供属性处理程序 (参阅下表中显示的 [**KSPROPERTY**](/previous-versions/ff564262(v=vs.85))) 。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">标记名称</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>KSPROPERTY_TYPE_GET</p></td>
<td align="left"><p>返回硬件 peakmeter 的当前值。</p></td>
</tr>
<tr class="even">
<td align="left"><p>KSPROPERTY_TYPE_BASICSUPPORT</p></td>
<td align="left"><p>
对于 KSPROPERTY_AUDIO_PEAKMETER-将0x8000 的数据范围返回到0x7fff，这是16位数字音频的数据范围。 高16位必须设置为零，以允许操作系统接收正值。 请注意，KSPROPERTY_AUDIO_PEAKMETER 已弃用，应改为使用 KSPROPERTY_AUDIO_PEAKMETER2。</p>
<p>对于 KSPROPERTY_AUDIO_PEAKMETER2-返回 LONG_MIN 的数据范围 LONG_MAX。</p>
</td>
</tr>
</tbody>
</table>

属性处理程序应验证输入参数和左和右通道信息。

Peakmeter 节点还应支持下表中的属性。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">属性名</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="ksproperty-audio-peakmeter2.md" data-raw-source="[&lt;strong&gt;KSPROPERTY_AUDIO_PEAKMETER2&lt;/strong&gt;](ksproperty-audio-peakmeter2.md)"><strong>KSPROPERTY_AUDIO_PEAKMETER2</strong></a></p></td>
<td align="left"><p>表示 peakmeter 控件。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ksproperty-audio-cpu-resources.md" data-raw-source="[&lt;strong&gt;KSPROPERTY_AUDIO_CPU_RESOURCES&lt;/strong&gt;](ksproperty-audio-cpu-resources.md)"><strong>KSPROPERTY_AUDIO_CPU_RESOURCES</strong></a></p></td>
<td align="left"><p>指示指定节点的功能是否利用了主机 CPU。</p></td>
</tr>
</tbody>
</table>