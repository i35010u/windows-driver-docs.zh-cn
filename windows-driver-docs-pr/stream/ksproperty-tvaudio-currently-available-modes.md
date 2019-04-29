---
title: KSPROPERTY\_TVAUDIO\_目前\_可用\_模式
description: KSPROPERTY\_TVAUDIO\_目前\_可用\_模式属性检索可用于设备的电视音频模式。 必须实现此属性。
ms.assetid: 9c98771a-7a41-469d-a441-da5c1ac5a697
keywords:
- KSPROPERTY_TVAUDIO_CURRENTLY_AVAILABLE_MODES 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_TVAUDIO_CURRENTLY_AVAILABLE_MODES
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5a4bd1450090346b39c9ff22802c9cb2f2a8c921
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63358214"
---
# <a name="kspropertytvaudiocurrentlyavailablemodes"></a>KSPROPERTY\_TVAUDIO\_目前\_可用\_模式


KSPROPERTY\_TVAUDIO\_目前\_可用\_模式属性检索可用于设备的电视音频模式。 必须实现此属性。

## <span id="ddk_ksproperty_tvaudio_currently_available_modes_ks"></span><span id="DDK_KSPROPERTY_TVAUDIO_CURRENTLY_AVAILABLE_MODES_KS"></span>


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
<td><p>否</p></td>
<td><p>Pin</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565953" data-raw-source="[&lt;strong&gt;KSPROPERTY_TVAUDIO_S&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565953)"><strong>KSPROPERTY_TVAUDIO_S</strong></a></p></td>
<td><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

属性值 （操作数据） 为 ULONG，指定当前可用电视音频模式，如立体声或单声道音频和多个语言设置。

<a name="remarks"></a>备注
-------

**模式下**KSPROPERTY 成员\_TVAUDIO\_S 结构指定的音频模式。 它包含 KS 按位 or 操作\_TVAUDIO\_模式\_\*信息已请求的标志，指出设备时支持的模式。

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

 

 






