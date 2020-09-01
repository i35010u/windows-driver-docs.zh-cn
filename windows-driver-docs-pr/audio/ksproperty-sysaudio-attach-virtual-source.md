---
title: KSPROPERTY \_ SYSAUDIO \_ 附加 \_ 虚拟 \_ 源
description: KSPROPERTY \_ SYSAUDIO \_ 附加 \_ 虚拟 \_ 源属性将虚拟源附加到虚拟音频设备上的 pin 实例。
ms.assetid: cb677eb2-b58d-4f36-b729-d0bfc06db07f
keywords:
- KSPROPERTY_SYSAUDIO_ATTACH_VIRTUAL_SOURCE 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_SYSAUDIO_ATTACH_VIRTUAL_SOURCE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5bdca4773eea64128c420693558f0007d659c7c1
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89206689"
---
# <a name="ksproperty_sysaudio_attach_virtual_source"></a>KSPROPERTY \_ SYSAUDIO \_ 附加 \_ 虚拟 \_ 源


KSPROPERTY \_ SYSAUDIO \_ 附加 \_ 虚拟 \_ 源属性将虚拟源附加到虚拟音频设备上的 pin 实例。

## <span id="ddk_ksproperty_sysaudio_attach_virtual_source_ks"></span><span id="DDK_KSPROPERTY_SYSAUDIO_ATTACH_VIRTUAL_SOURCE_KS"></span>


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
<td align="left"><p>是</p></td>
<td align="left"><p>Pin</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-sysaudio_attach_virtual_source" data-raw-source="[&lt;strong&gt;SYSAUDIO_ATTACH_VIRTUAL_SOURCE&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-sysaudio_attach_virtual_source)"><strong>SYSAUDIO_ATTACH_VIRTUAL_SOURCE</strong></a></p></td>
<td align="left"><p>无</p></td>
</tr>
</tbody>
</table>

 

 (实例数据) 的属性描述符是 \_ \_ \_ 指定属性和虚拟源索引的 SYSAUDIO 附加虚拟源类型的结构。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY \_ SYSAUDIO \_ 附加 \_ 虚拟 \_ 源属性请求返回状态 \_ SUCCESS 以指示已成功完成。 否则，请求将返回相应的错误状态代码。

<a name="remarks"></a>备注
-------

此属性将虚拟源附加到虚拟音频设备上的 pin 实例。 有关详细信息，请参阅 [**KSPROPERTY \_ SYSAUDIO \_ CREATE \_ VIRTUAL \_ SOURCE**](ksproperty-sysaudio-create-virtual-source.md)。

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


[**SYSAUDIO \_ 附加 \_ 虚拟 \_ 源**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-sysaudio_attach_virtual_source)

[**KSPROPERTY \_ SYSAUDIO \_ 创建 \_ 虚拟 \_ 源**](ksproperty-sysaudio-create-virtual-source.md)

 

