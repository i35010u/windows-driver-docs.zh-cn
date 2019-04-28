---
title: KSPROPERTY\_RTAUDIO\_POSITIONREGISTER
description: KSPROPERTY\_RTAUDIO\_POSITIONREGISTER 属性映射到客户端可以访问的虚拟内存位置的特定流的音频设备的位置寄存器。下表总结了此属性的功能。
ms.assetid: 812072ec-d2a5-4e84-aebe-f24ca0d3cb21
keywords:
- KSPROPERTY_RTAUDIO_POSITIONREGISTER Audio Devices
topic_type:
- apiref
api_name:
- KSPROPERTY_RTAUDIO_POSITIONREGISTER
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: fabefcd7ecaddb9efed29cf16c47b9fb6c2ff83e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332668"
---
# <a name="kspropertyrtaudiopositionregister"></a>KSPROPERTY\_RTAUDIO\_POSITIONREGISTER


KSPROPERTY\_RTAUDIO\_POSITIONREGISTER 属性映射到客户端可以访问的虚拟内存位置的特定流的音频设备的位置寄存器。

下表总结了此属性的功能。

### <a name="span-idusagesummarytablespanspan-idusagesummarytablespanspan-idusagesummarytablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用率摘要表

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Get</th>
<th align="left">设置</th>
<th align="left">目标</th>
<th align="left">属性描述符类型</th>
<th align="left">属性值类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>是</p></td>
<td align="left"><p>否</p></td>
<td align="left"><p>Pin</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff537498" data-raw-source="[&lt;strong&gt;KSRTAUDIO_HWREGISTER_PROPERTY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537498)"><strong>KSRTAUDIO_HWREGISTER_PROPERTY</strong></a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff537497" data-raw-source="[&lt;strong&gt;KSRTAUDIO_HWREGISTER&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537497)"><strong>KSRTAUDIO_HWREGISTER</strong></a></p></td>
</tr>
</tbody>
</table>

 

属性描述符 （实例数据） 是 KSRTAUDIO\_HWREGISTER\_属性结构，其中包含[ **KSPROPERTY** ](https://msdn.microsoft.com/library/windows/hardware/ff564262)结构。 发送请求之前, 在客户端加载用来指示寄存器的首选基址的值的结构。

属性值 （操作数据） 是 KSRTAUDIO\_HWREGISTER 结构到其中的属性处理程序写入其具有硬件映射到的虚拟地址位置注册。 客户端可以直接读取此地址注册。 KSRTAUDIO\_HWREGISTER 结构还指定了位置注册自身都会的递增的速率。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY\_RTAUDIO\_POSITIONREGISTER 属性请求将返回状态\_成功以指示已成功完成。 否则，请求将返回相应的故障状态代码。

<a name="remarks"></a>备注
-------

通常情况下，音频的应用程序必须监视的音频流的当前位置。 此位置指定为从流开头的字节偏移量：

-   对于呈现流、 流的位置是通过数字模拟转换器 (Dac) 当前正在播放的音频帧的字节偏移量。

-   对于捕获流、 流的位置是当前正在通过模拟到数字转换器 (ADCs) 录制的音频帧的字节偏移量。

一些音频设备包含不断运行流时递增的位置寄存器。 将所有数字和模拟功能合并到单个芯片的音频设备，对于位置注册都直接通常指示当前流位置。

但是，对于将数字和模拟功能划分为单独的总线控制器和编解码器芯片芯片组，位置注册通常位于总线控制器芯片和如下所示：

-   在呈现流的情况下位置注册指示最后一个总线控制器已写入到编解码器的音频帧的字节偏移量。

-   在捕获流的情况下位置注册指示最后一个总线控制器读取编解码器的音频帧的字节偏移量。

在这两种情况下，位置寄存器值不包括通过编解码器的延迟。 如果客户端已确定的编解码器延迟，它可以将这种延迟添加到位置寄存器值 （在 Dac 或 ADCs） 估计 true 流的位置。 有关 CodecDelay 值，该值指定通过编解码器的最坏的情况延迟，可以查询[ **KSPROPERTY\_RTAUDIO\_HWLATENCY** ](ksproperty-rtaudio-hwlatency.md)属性。

如果成功，KSPROPERTY\_RTAUDIO\_POSITIONREGISTER 属性请求映射到可向客户端从用户模式或内核模式下指定的客户端访问的虚拟内存地址位置注册。 此后，客户端读取来自该地址以获取位置注册的当前值。

如果音频硬件不支持可以映射到的虚拟地址位置注册，失败属性请求。 在这种情况下，客户端必须确定数据的位置[ **KSPROPERTY\_音频\_位置**](ksproperty-audio-position.md)属性。

Pin 关闭时，将销毁位置注册的映射。 客户端可以在打开的 pin，生命周期的映射仅一次的寄存器和任何后续调用以重新映射位置注册 pin 失败。

它是通常更快地读取位置注册比发送 KSPROPERTY\_音频\_位置请求，这就需要为用户模式下客户端的用户模式和内核模式之间的转换。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Version</p></td>
<td align="left"><p>在 Windows Vista 和更高版本的 Windows 操作系统中可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Ksmedia.h</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**KSPROPERTY**](https://msdn.microsoft.com/library/windows/hardware/ff564262)

[**KSRTAUDIO\_HWREGISTER**](https://msdn.microsoft.com/library/windows/hardware/ff537497)

[**KSRTAUDIO\_HWREGISTER\_PROPERTY**](https://msdn.microsoft.com/library/windows/hardware/ff537498)

[**KSPROPERTY\_音频\_位置**](ksproperty-audio-position.md)

[**KSPROPERTY\_RTAUDIO\_HWLATENCY**](ksproperty-rtaudio-hwlatency.md)

 

 






