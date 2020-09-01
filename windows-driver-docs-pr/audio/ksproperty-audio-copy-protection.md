---
title: KSPROPERTY \_ 音频 \_ 复制 \_ 保护
description: KSPROPERTY \_ audio \_ copy \_ protection 属性指定音频流的复制保护状态。
ms.assetid: 68896bd4-9ffe-4632-a3b2-441b5d04208a
keywords:
- KSPROPERTY_AUDIO_COPY_PROTECTION 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIO_COPY_PROTECTION
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ca554267409d8760cded8bc2bd8ce7ea832c1354
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89208993"
---
# <a name="ksproperty_audio_copy_protection"></a>KSPROPERTY \_ 音频 \_ 复制 \_ 保护


KSPROPERTY \_ audio \_ copy \_ protection 属性指定音频流的复制保护状态。

## <span id="ddk_ksproperty_audio_copy_protection_ks"></span><span id="DDK_KSPROPERTY_AUDIO_COPY_PROTECTION_KS"></span>


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
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/ff564262(v=vs.85)" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](/previous-versions/ff564262(v=vs.85))"><strong>KSPROPERTY</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksaudio_copy_protection" data-raw-source="[&lt;strong&gt;KSAUDIO_COPY_PROTECTION&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksaudio_copy_protection)"><strong>KSAUDIO_COPY_PROTECTION</strong></a></p></td>
</tr>
</tbody>
</table>

 

 (操作数据) 的属性值是 KSAUDIO COPY PROTECTION 类型的 \_ 结构 \_ 。 结构指定流是否受版权保护;它还指定流是原始流还是原始流的副本。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY \_ 音频 \_ 复制 \_ 保护属性请求返回状态 " \_ 成功" 以指示已成功完成。 否则，请求将返回相应的错误状态代码。

<a name="remarks"></a>备注
-------

KSPROPERTY \_ 音频 \_ 复制 \_ 保护属性是音频设备的一个属性，它支持类似于串行复制管理系统 (SCMS) 的保护方案。 属性指示数字流是否受版权保护，以及它是原始流还是副本。

SCMS 可以提供三个级别的音频内容保护：

**级别0：** 无限制复制不受版权限制或未断言版权的流。

**级别1：** 复制到第一代流的限制。 用户可以创建具有原始版权保护的流的副本，但不能创建流副本副本。

**级别2：** 所有流都不复制。

KSPROPERTY \_ audio \_ COPY \_ PROTECTION 属性与 [数字 Rights Management (DRM) ](./digital-rights-management.md) 和 (SAP) For Windows Media 的安全音频路径的实现不同。 有关 SAP 的信息，请参阅 Microsoft Windows SDK 文档。

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


[**KSPROPERTY**](/previous-versions/ff564262(v=vs.85))

[**KSAUDIO \_ 复制 \_ 保护**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksaudio_copy_protection)

 

