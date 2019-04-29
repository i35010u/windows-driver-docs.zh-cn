---
title: KSPROPERTY\_TVAUDIO\_CAP
description: KSPROPERTY\_TVAUDIO\_CAPS 属性检索电视音频设备的功能。 必须实现此属性。
ms.assetid: a5b7348e-0f85-430c-acf0-c35e289ef338
keywords:
- KSPROPERTY_TVAUDIO_CAPS 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_TVAUDIO_CAPS
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3076ba9914a91537af3cb7940f0c96502da1e8b5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63382546"
---
# <a name="kspropertytvaudiocaps"></a>KSPROPERTY\_TVAUDIO\_CAP


KSPROPERTY\_TVAUDIO\_CAPS 属性检索电视音频设备的功能。 必须实现此属性。

## <span id="ddk_ksproperty_tvaudio_caps_ks"></span><span id="DDK_KSPROPERTY_TVAUDIO_CAPS_KS"></span>


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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565936" data-raw-source="[&lt;strong&gt;KSPROPERTY_TVAUDIO_CAPS_S&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565936)"><strong>KSPROPERTY_TVAUDIO_CAPS_S</strong></a></p></td>
<td><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

属性值 （操作数据） 为指定的电视音频设备，例如与单声道音频支持与多个语言功能的立体声功能的 ULONG。

<a name="remarks"></a>备注
-------

**功能**KSPROPERTY 成员\_TVAUDIO\_CAPS\_S 结构指定电视音频设备的功能。

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

[**KSPROPERTY\_TVAUDIO\_CAPS\_S**](https://msdn.microsoft.com/library/windows/hardware/ff565936)

 

 






