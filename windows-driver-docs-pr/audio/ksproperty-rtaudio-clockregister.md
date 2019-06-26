---
title: KSPROPERTY\_RTAUDIO\_CLOCKREGISTER
description: KSPROPERTY\_RTAUDIO\_CLOCKREGISTER 属性会映射到客户端可以访问的虚拟内存位置的音频设备的墙时钟寄存器。 下表总结了此属性的功能。
ms.assetid: a35b5830-55e4-4e92-a4f1-df9edcc2f5bb
keywords:
- KSPROPERTY_RTAUDIO_CLOCKREGISTER 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_RTAUDIO_CLOCKREGISTER
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: dd9304c59a33c2a40882d090ec0d80757dc36722
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354391"
---
# <a name="kspropertyrtaudioclockregister"></a>KSPROPERTY\_RTAUDIO\_CLOCKREGISTER


KSPROPERTY\_RTAUDIO\_CLOCKREGISTER 属性会映射到客户端可以访问的虚拟内存位置的音频设备的墙时钟寄存器。

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksrtaudio_hwregister_property" data-raw-source="[&lt;strong&gt;KSRTAUDIO_HWREGISTER_PROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksrtaudio_hwregister_property)"><strong>KSRTAUDIO_HWREGISTER_PROPERTY</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksrtaudio_hwregister" data-raw-source="[&lt;strong&gt;KSRTAUDIO_HWREGISTER&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksrtaudio_hwregister)"><strong>KSRTAUDIO_HWREGISTER</strong></a></p></td>
</tr>
</tbody>
</table>

 

属性描述符 （实例数据） 包含 KSRTAUDIO\_HWREGISTER\_属性结构，其中包含[ **KSPROPERTY** ](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85))结构。 发送请求之前, 在客户端加载 KSRTAUDIO\_HWREGISTER\_属性结构指示时钟注册的首选基址的值。

（操作数据） 的属性值是指向 KSRTAUDIO\_HWREGISTER 结构的属性处理程序将注册地址和注册更新频率写入到其中。 此注册地址是硬件注册映射到的用户模式或内核模式虚拟地址。 客户端可以直接读取此地址注册。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY\_RTAUDIO\_CLOCKREGISTER 属性请求将返回状态\_成功以指示已成功完成。 否则，请求将返回错误代码指示失败的。

<a name="remarks"></a>备注
-------

一些音频设备包含时钟寄存器。 时钟注册是一个开始运行时的硬件将启动和停止时硬件电源将关闭的墙时钟计数器。 软件使用时钟注册以通过测量设备的硬件时钟之间的相对偏移的两个或多个控制器设备之间进行同步。

如果成功，属性请求将时钟注册映射到可从用户模式或内核模式下指定的客户端访问的虚拟内存地址。 此后，客户端读取来自该地址来获取当前时钟寄存器的值。

如果音频硬件不支持可以映射到虚拟内存的时钟寄存器，属性请求失败。

Pin 关闭时，将销毁时钟寄存器的映射。 客户端可以将注册一次只能映射生存期内的一个 pin 的实例，并映射该实例再次时钟注册任何后续调用将失败。

它是通常更快地读取时钟注册比发送[ **KSPROPERTY\_时钟\_时间**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-clock-time)请求，这要求用户模式和内核模式的之间的转换用户模式下客户端。

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


[**KSRTAUDIO\_HWREGISTER\_PROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksrtaudio_hwregister_property)

[**KSRTAUDIO\_HWREGISTER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksrtaudio_hwregister)

 

 






