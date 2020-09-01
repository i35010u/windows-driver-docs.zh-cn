---
title: KSPROPERTY \_ DIRECTSOUND3DBUFFER \_ MINDISTANCE
description: KSPROPERTY \_ DIRECTSOUND3DBUFFER \_ MINDISTANCE 属性指定三维声音缓冲区的最小距离。
ms.assetid: 998e591d-7c23-4857-908c-4e90918c9a94
keywords:
- KSPROPERTY_DIRECTSOUND3DBUFFER_MINDISTANCE 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_DIRECTSOUND3DBUFFER_MINDISTANCE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2f156ce922652c4bc9c4eb7992052bca41981965
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89206877"
---
# <a name="ksproperty_directsound3dbuffer_mindistance"></a>KSPROPERTY \_ DIRECTSOUND3DBUFFER \_ MINDISTANCE


KSPROPERTY \_ DIRECTSOUND3DBUFFER \_ MINDISTANCE 属性指定三维声音缓冲区的最小距离。

## <span id="ddk_ksproperty_directsound3dbuffer_mindistance_ks"></span><span id="DDK_KSPROPERTY_DIRECTSOUND3DBUFFER_MINDISTANCE_KS"></span>


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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty)"><strong>KSNODEPROPERTY</strong></a></p></td>
<td align="left"><p>FLOAT</p></td>
</tr>
</tbody>
</table>

 

 (操作数据) 的属性值为 FLOAT 类型，并指定最小距离。 有关距离单位的信息，请参阅 [**KSPROPERTY \_ DIRECTSOUND3DLISTENER \_ DISTANCEFACTOR**](ksproperty-directsound3dlistener-distancefactor.md)。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY \_ DIRECTSOUND3DBUFFER \_ MINDISTANCE 属性请求返回状态 \_ SUCCESS 以指示该请求已成功完成。 否则，请求将返回相应的错误状态代码。

<a name="remarks"></a>备注
-------

在小于与声音源的最小距离的距离上，当距离下降时，音量不再增加。 有关 DirectSound 3D 缓冲区的最小距离的详细信息，请参阅 Microsoft Windows SDK 文档中的以下内容：

-   DS3DBUFFER 结构的 **flMinDistance** 成员。

-   **IDirectSound3DBuffer：： GetMinDistance**和**IDirectSound3DBuffer：： SetMinDistance**方法。

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

[**KSPROPERTY \_ DIRECTSOUND3DLISTENER \_ DISTANCEFACTOR**](ksproperty-directsound3dlistener-distancefactor.md)

 

