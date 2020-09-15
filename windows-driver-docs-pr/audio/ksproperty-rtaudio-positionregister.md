---
title: KSPROPERTY \_ RTAUDIO \_ POSITIONREGISTER
description: KSPROPERTY \_ RTAUDIO \_ POSITIONREGISTER 属性将特定流的音频设备位置注册映射到客户端可以访问的虚拟内存位置。下表汇总了此属性的功能。
ms.assetid: 812072ec-d2a5-4e84-aebe-f24ca0d3cb21
keywords:
- KSPROPERTY_RTAUDIO_POSITIONREGISTER 音频设备
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
ms.openlocfilehash: f1d76bb19d63beb50586caa11422512bda1f9738
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90101942"
---
# <a name="ksproperty_rtaudio_positionregister"></a>KSPROPERTY \_ RTAUDIO \_ POSITIONREGISTER


KSPROPERTY \_ RTAUDIO \_ POSITIONREGISTER 属性将特定流的音频设备位置注册映射到客户端可以访问的虚拟内存位置。

下表汇总了此属性的功能。

### <a name="span-idusage_summary_tablespanspan-idusage_summary_tablespanspan-idusage_summary_tablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用情况摘要表

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
<th align="left">获取</th>
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
<td align="left"><p><a href="/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksrtaudio_hwregister_property" data-raw-source="[&lt;strong&gt;KSRTAUDIO_HWREGISTER_PROPERTY&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksrtaudio_hwregister_property)"><strong>KSRTAUDIO_HWREGISTER_PROPERTY</strong></a></p></td>
<td align="left"><p><a href="/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksrtaudio_hwregister" data-raw-source="[&lt;strong&gt;KSRTAUDIO_HWREGISTER&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksrtaudio_hwregister)"><strong>KSRTAUDIO_HWREGISTER</strong></a></p></td>
</tr>
</tbody>
</table>

 

属性描述符 (实例数据) 是 KSRTAUDIO \_ HWREGISTER \_ 属性结构，其中包含 [**KSPROPERTY**](/previous-versions/ff564262(v=vs.85)) 结构。 在发送请求之前，客户端将加载包含指示寄存器首选基址的值的结构。

 (操作数据) 的属性值是一个 KSRTAUDIO \_ HWREGISTER 结构，属性处理程序会将其映射到的虚拟地址写入硬件位置寄存器。 客户端可以直接从该地址读取寄存器。 KSRTAUDIO \_ HWREGISTER 结构还指定了位置寄存器的增量。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY \_ RTAUDIO \_ POSITIONREGISTER 属性请求返回状态 \_ SUCCESS 以指示该请求已成功完成。 否则，请求将返回相应的失败状态代码。

<a name="remarks"></a>注解
-------

通常，音频应用程序必须监视音频流的当前位置。 此位置被指定为距流开头的字节偏移量：

-   对于呈现流，流的位置是当前通过数字到模拟转换器播放的音频帧的字节偏移量 (Dac) 。

-   对于捕获流，流的位置是当前通过模拟到数字转换器录制的音频帧的字节偏移量 (ADCs) 。

某些音频设备包含在流运行时连续递增的位置寄存器。 对于将所有数字和模拟功能合并到单个芯片中的音频设备，位置寄存器通常直接指示当前的流位置。

但是，对于将数字和模拟功能分割为单独的总线控制器和编解码器芯片的芯片组，位置寄存器通常位于总线控制器芯片中，表示以下内容：

-   对于呈现流，位置寄存器指示总线控制器写入编解码器的最后一个音频帧的字节偏移量。

-   对于捕获流，位置寄存器指示总线控制器从编解码器读取的最后一个音频帧的字节偏移量。

在这两种情况下，位置寄存器值都不包括经过编解码器的延迟。 如果客户端已确定编解码器延迟，则可以将此延迟添加到位置寄存器值，以估计 Dac 或 ADCs) 处 (的真实流位置。 对于通过编解码器指定最坏情况延迟的 CodecDelay 值，可以查询 [**KSPROPERTY \_ RTAUDIO \_ HWLATENCY**](ksproperty-rtaudio-hwlatency.md) 属性。

如果成功，KSPROPERTY \_ RTAUDIO \_ POSITIONREGISTER 属性请求会将位置寄存器映射到客户端根据客户端指定的用户模式或内核模式可访问的虚拟内存地址。 此后，客户端将从此地址读取以获取位置注册的当前值。

如果音频硬件不支持可映射到虚拟地址的位置注册，则属性请求失败。 在这种情况下，客户端必须确定 [**KSPROPERTY \_ 音频 \_ 位置**](ksproperty-audio-position.md) 属性中的位置。

当 pin 关闭时，位置寄存器的映射将被销毁。 在打开的 pin 的生存期内，客户端只能映射一次注册，并且对重映射位置注册的任何后续调用都将失败。

通常，读取位置注册的速度比发送 KSPROPERTY 音频位置请求的速度更 \_ 快 \_ ，要求用户模式客户端的用户模式和内核模式之间转换。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>版本</p></td>
<td align="left"><p>在 Windows Vista 和更高版本的 Windows 操作系统中可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">Ksmedia.h</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**KSPROPERTY**](/previous-versions/ff564262(v=vs.85))

[**KSRTAUDIO \_ HWREGISTER**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksrtaudio_hwregister)

[**KSRTAUDIO \_ HWREGISTER \_ 属性**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksrtaudio_hwregister_property)

[**KSPROPERTY \_ 音频 \_ 位置**](ksproperty-audio-position.md)

[**KSPROPERTY \_ RTAUDIO \_ HWLATENCY**](ksproperty-rtaudio-hwlatency.md)

