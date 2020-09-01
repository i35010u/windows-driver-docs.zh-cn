---
title: KSPROPERTY \_ 音频 \_ CPU \_ 资源
description: "\"KSPROPERTY \\_ 音频 \\_ CPU \\_ 资源\" 属性指定是在硬件中实现节点的功能，还是在主机 CPU 上运行的软件中对其进行模拟。"
ms.assetid: 4379aa05-9661-44cd-8f10-0fb37009a4f3
keywords:
- KSPROPERTY_AUDIO_CPU_RESOURCES 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIO_CPU_RESOURCES
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4700dd2c3349286ee4c9073a3baf04efa690f099
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89208995"
---
# <a name="ksproperty_audio_cpu_resources"></a>KSPROPERTY \_ 音频 \_ CPU \_ 资源


"KSPROPERTY \_ 音频 \_ CPU \_ 资源" 属性指定是在硬件中实现节点的功能，还是在主机 CPU 上运行的软件中对其进行模拟。

## <span id="ddk_ksproperty_audio_cpu_resources_ks"></span><span id="DDK_KSPROPERTY_AUDIO_CPU_RESOURCES_KS"></span>


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
<td align="left"><p>筛选器</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty)"><strong>KSNODEPROPERTY</strong></a></p></td>
<td align="left"><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

 (操作数据) 的属性值为 ULONG 类型，指示节点的功能是否在硬件或软件中实现。 微型端口驱动程序将此值设置为标头文件 Ksmedia 中的以下两个常量之一：

<span id="KSAUDIO_CPU_RESOURCES_HOST_CPU"></span><span id="ksaudio_cpu_resources_host_cpu"></span>KSAUDIO \_ CPU \_ 资源 \_ 主机 \_ CPU  
此节点在主机 CPU 上运行的软件中实现其功能。

<span id="KSAUDIO_CPU_RESOURCES_NOT_HOST_CPU"></span><span id="ksaudio_cpu_resources_not_host_cpu"></span>KSAUDIO \_ CPU \_ 资源 \_ 不 \_ 承载 \_ CPU  
此节点在硬件中实现其功能。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY \_ 音频 \_ CPU \_ 资源属性请求返回状态 " \_ 成功" 以指示已成功完成。 否则，请求将返回相应的错误状态代码。

<a name="remarks"></a>备注
-------

此属性用于确定是否在硬件或软件中实现以下节点类型：

-   AEC 节点 ([**KSNODETYPE 的 \_ 声音 \_ 回声 \_ 取消**](ksnodetype-acoustic-echo-cancel.md)) 

-   干扰禁止节点 ([**KSNODETYPE \_ 干扰 \_ **](ksnodetype-noise-suppress.md)) 

-   Peakmeter 节点 ([**KSNODETYPE \_ Peakmeter**](ksnodetype-peakmeter.md)) 

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>标头</p></td>
<td align="left">Ksmedia (包含 Ksmedia) </td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**KSNODEPROPERTY**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty)

[**KSNODETYPE \_ 回声 \_ \_ 取消**](ksnodetype-acoustic-echo-cancel.md)

[**KSNODETYPE \_ 干扰 \_**](ksnodetype-noise-suppress.md)

[**KSNODETYPE \_ PEAKMETER**](ksnodetype-peakmeter.md)

 

