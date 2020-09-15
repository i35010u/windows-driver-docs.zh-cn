---
title: KSPROPERTY \_ SYSAUDIO \_ 实例 \_ 信息
description: KSPROPERTY \_ SYSAUDIO \_ 实例 \_ 信息属性打开一个虚拟音频设备，并指定该设备的配置标志。
ms.assetid: ef60c188-704f-4dbb-bf6d-cdf3152c209b
keywords:
- KSPROPERTY_SYSAUDIO_INSTANCE_INFO 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_SYSAUDIO_INSTANCE_INFO
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0c0734df695ec4d3a3d20def6811356c061d3c46
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90101864"
---
# <a name="ksproperty_sysaudio_instance_info"></a>KSPROPERTY \_ SYSAUDIO \_ 实例 \_ 信息


KSPROPERTY \_ SYSAUDIO \_ 实例 \_ 信息属性打开一个虚拟音频设备，并指定该设备的配置标志。

## <span id="ddk_ksproperty_sysaudio_instance_info_ks"></span><span id="DDK_KSPROPERTY_SYSAUDIO_INSTANCE_INFO_KS"></span>


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
<td align="left"><p>筛选器</p></td>
<td align="left"><p><a href="/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-sysaudio_instance_info" data-raw-source="[&lt;strong&gt;SYSAUDIO_INSTANCE_INFO&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-sysaudio_instance_info)"><strong>SYSAUDIO_INSTANCE_INFO</strong></a></p></td>
<td align="left"><p>无</p></td>
</tr>
</tbody>
</table>

 

 (实例数据) 的属性描述符是 SYSAUDIO 实例信息类型的 \_ 结构 \_ ，它指定要打开的虚拟音频设备，同时还指定该设备的配置标志。

没有为此属性定义 (操作数据) 的属性值。 将属性值指针指定为 **NULL**，将属性值大小指定为零。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY \_ SYSAUDIO \_ 实例 \_ 信息属性请求返回状态 " \_ 成功" 以指示它已成功完成。 否则，请求将返回相应的错误状态代码。

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


[**SYSAUDIO \_ 实例 \_ 信息**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-sysaudio_instance_info)

