---
title: KSPROPERTY \_ RTAUDIO \_ CLOCKREGISTER
description: KSPROPERTY \_ RTAUDIO \_ CLOCKREGISTER 属性将音频设备的墙壁时钟寄存器映射到客户端可以访问的虚拟内存位置。 下表汇总了此属性的功能。
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
ms.openlocfilehash: 86dd5560868460cc3d2dd99f1fedef261aae778a
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89210951"
---
# <a name="ksproperty_rtaudio_clockregister"></a>KSPROPERTY \_ RTAUDIO \_ CLOCKREGISTER


KSPROPERTY \_ RTAUDIO \_ CLOCKREGISTER 属性将音频设备的墙壁时钟寄存器映射到客户端可以访问的虚拟内存位置。

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksrtaudio_hwregister_property" data-raw-source="[&lt;strong&gt;KSRTAUDIO_HWREGISTER_PROPERTY&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksrtaudio_hwregister_property)"><strong>KSRTAUDIO_HWREGISTER_PROPERTY</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksrtaudio_hwregister" data-raw-source="[&lt;strong&gt;KSRTAUDIO_HWREGISTER&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksrtaudio_hwregister)"><strong>KSRTAUDIO_HWREGISTER</strong></a></p></td>
</tr>
</tbody>
</table>

 

属性描述符 (实例数据) 由 \_ \_ 包含 [**KSPROPERTY**](/previous-versions/ff564262(v=vs.85)) 结构的 KSRTAUDIO HWREGISTER 属性结构构成。 在发送请求之前，客户端会加载 KSRTAUDIO \_ HWREGISTER \_ 属性结构，其值指示时钟寄存器的首选基址。

) 操作数据 (的属性值是一个指向 KSRTAUDIO HWREGISTER 结构的指针， \_ 属性处理程序会将该结构写入注册地址和注册更新频率。 此注册地址是硬件注册映射到的用户模式或内核模式的虚拟地址。 客户端可以直接从该地址读取寄存器。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY \_ RTAUDIO \_ CLOCKREGISTER 属性请求返回状态 \_ SUCCESS 以指示该请求已成功完成。 否则，请求将返回指示失败的错误代码。

<a name="remarks"></a>备注
-------

某些音频设备包含时钟寄存器。 时钟寄存器是一个时钟计数器，它在硬件启动时开始运行并在硬件关闭时停止运行。 通过测量设备硬件时钟之间的相对偏差，软件使用时钟寄存器在两个或更多控制器设备之间进行同步。

如果成功，属性请求会将时钟寄存器映射到可从用户模式或内核模式（由客户端指定）访问的虚拟内存地址。 此后，客户端将从此地址读取以获取时钟寄存器的当前值。

如果音频硬件不支持可映射到虚拟内存的时钟寄存器，则属性请求失败。

当 pin 关闭时，时钟寄存器的映射会被销毁。 客户端可以在 pin 实例的生存期内仅映射一次注册，并对该实例再次映射时钟注册失败。

通常，读取时钟寄存器的速度比发送 [**KSPROPERTY \_ 时钟 \_ 时间**](../stream/ksproperty-clock-time.md) 请求要快，后者要求用户模式客户端模式和内核模式间的转换。

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


[**KSRTAUDIO \_ HWREGISTER \_ 属性**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksrtaudio_hwregister_property)

[**KSRTAUDIO \_ HWREGISTER**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksrtaudio_hwregister)

 

