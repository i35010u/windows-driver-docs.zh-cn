---
title: KSPROPERTY\_音频\_CPU\_资源
description: KSPROPERTY\_音频\_CPU\_资源属性指定是否在硬件中实现节点的功能，或在主机 CPU 上运行的软件中进行模拟。
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
ms.openlocfilehash: 286e988e4bf16c20b016cba464270a9b4c10e500
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831051"
---
# <a name="ksproperty_audio_cpu_resources"></a>KSPROPERTY\_音频\_CPU\_资源


KSPROPERTY\_音频\_CPU\_资源属性指定是否在硬件中实现节点的功能，或在主机 CPU 上运行的软件中进行模拟。

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
<th align="left">“获取”</th>
<th align="left">设置</th>
<th align="left">目标</th>
<th align="left">属性描述符类型</th>
<th align="left">属性值类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>“是”</p></td>
<td align="left"><p>无</p></td>
<td align="left"><p>Filter</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty)"><strong>KSNODEPROPERTY</strong></a></p></td>
<td align="left"><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

属性值（操作数据）的类型为 ULONG，指示节点的功能是否在硬件或软件中实现。 微型端口驱动程序将此值设置为标头文件 Ksmedia 中的以下两个常量之一：

<span id="KSAUDIO_CPU_RESOURCES_HOST_CPU"></span><span id="ksaudio_cpu_resources_host_cpu"></span>KSAUDIO\_CPU\_资源\_主机\_CPU  
此节点在主机 CPU 上运行的软件中实现其功能。

<span id="KSAUDIO_CPU_RESOURCES_NOT_HOST_CPU"></span><span id="ksaudio_cpu_resources_not_host_cpu"></span>KSAUDIO\_CPU\_资源\_不\_主机\_CPU  
此节点在硬件中实现其功能。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY\_音频\_CPU\_资源属性请求返回状态\_"成功" 以指示已成功完成。 否则，请求将返回相应的错误状态代码。

<a name="remarks"></a>备注
-------

此属性用于确定是否在硬件或软件中实现以下节点类型：

-   AEC 节点（[**KSNODETYPE\_声音\_回音\_取消**](ksnodetype-acoustic-echo-cancel.md)）

-   干扰-抑制节点（[**KSNODETYPE\_显示\_抑制**](ksnodetype-noise-suppress.md)）

-   Peakmeter 节点（[**KSNODETYPE\_Peakmeter**](ksnodetype-peakmeter.md)）

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
<td align="left">Ksmedia （包括 Ksmedia）</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**KSNODEPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty)

[**KSNODETYPE\_声音\_回音\_取消**](ksnodetype-acoustic-echo-cancel.md)

[**KSNODETYPE\_\_禁止显示**](ksnodetype-noise-suppress.md)

[**KSNODETYPE\_PEAKMETER**](ksnodetype-peakmeter.md)

 

 






