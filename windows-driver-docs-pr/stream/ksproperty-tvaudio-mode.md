---
title: KSPROPERTY\_TVAUDIO\_MODE
description: KSPROPERTY\_TVAUDIO\_模式属性设置为设备的音频模式。 必须实现此属性。
ms.assetid: ef2db4b9-307f-4f70-8c9f-1344420c8cba
keywords:
- KSPROPERTY_TVAUDIO_MODE 流式处理媒体设备
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
ms.openlocfilehash: f5905d194337034c9b1bb46b9cdb817d87289812
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63355537"
---
# <a name="kspropertytvaudiomode"></a>KSPROPERTY\_TVAUDIO\_MODE


KSPROPERTY\_TVAUDIO\_模式属性设置为设备的音频模式。 必须实现此属性。

## <span id="ddk_ksproperty_tvaudio_mode_ks"></span><span id="DDK_KSPROPERTY_TVAUDIO_MODE_KS"></span>


### <a name="usage-summary-table"></a>使用率摘要表

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
<th>Get</th>
<th>设置</th>
<th>目标</th>
<th>属性描述符类型</th>
<th>属性值类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>Pin</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565953" data-raw-source="[&lt;strong&gt;KSPROPERTY_TVAUDIO_S&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565953)"><strong>KSPROPERTY_TVAUDIO_S</strong></a></p></td>
<td><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

属性值 （操作数据） 为 ULONG，用于指定当前电视音频模式，如立体声或单声道音频和语言设置。

<a name="remarks"></a>备注
-------

**模式下**KSPROPERTY 成员\_TVAUDIO\_S 结构指定的音频模式。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Ksmedia.h （包括 Ksmedia.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)

[**KSPROPERTY\_TVAUDIO\_S**](https://msdn.microsoft.com/library/windows/hardware/ff565953)

 

 






