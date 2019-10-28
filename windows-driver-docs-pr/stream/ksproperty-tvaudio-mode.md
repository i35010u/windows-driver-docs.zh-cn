---
title: KSPROPERTY\_TVAUDIO\_模式
description: KSPROPERTY\_TVAUDIO\_模式属性设置设备的音频模式。 必须实现此属性。
ms.assetid: ef2db4b9-307f-4f70-8c9f-1344420c8cba
keywords:
- KSPROPERTY_TVAUDIO_MODE 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_TVAUDIO_MODE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4915954b56e08fb94d3d9371544245e7a4e16e99
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837892"
---
# <a name="ksproperty_tvaudio_mode"></a>KSPROPERTY\_TVAUDIO\_模式


KSPROPERTY\_TVAUDIO\_模式属性设置设备的音频模式。 必须实现此属性。

## <span id="ddk_ksproperty_tvaudio_mode_ks"></span><span id="DDK_KSPROPERTY_TVAUDIO_MODE_KS"></span>


### <a name="usage-summary-table"></a>使用情况摘要表

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
<th>“获取”</th>
<th>设置</th>
<th>目标</th>
<th>属性描述符类型</th>
<th>属性值类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>“是”</p></td>
<td><p>“是”</p></td>
<td><p>大头针</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tvaudio_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_TVAUDIO_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tvaudio_s)"><strong>KSPROPERTY_TVAUDIO_S</strong></a></p></td>
<td><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

属性值（操作数据）是一个 ULONG，指定当前电视音频模式，如立体声或 mono 音频和语言设置。

<a name="remarks"></a>备注
-------

KSPROPERTY\_TVAUDIO\_S 结构的**Mode**成员指定音频模式。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>标头</p></td>
<td>Ksmedia （包括 Ksmedia）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)

[**KSPROPERTY\_TVAUDIO\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tvaudio_s)

 

 






