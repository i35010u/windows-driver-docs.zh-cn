---
title: KSPROPERTY\_ATN\_READER
description: KSPROPERTY\_ATN\_读取器属性检索当前磁带位置的绝对跟踪数 (ATN)。
ms.assetid: ac127aa0-5a47-41b2-9a2d-96090231d43e
keywords:
- KSPROPERTY_ATN_READER 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_ATN_READER
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c25a4972986d34953cfafcd76f910f224d153c46
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63384152"
---
# <a name="kspropertyatnreader"></a>KSPROPERTY\_ATN\_READER


KSPROPERTY\_ATN\_读取器属性检索当前磁带位置的绝对跟踪数 (ATN)。

## <span id="ddk_ksproperty_atn_reader_ks"></span><span id="DDK_KSPROPERTY_ATN_READER_KS"></span>


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
<td><p>设备</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565781" data-raw-source="[&lt;strong&gt;KSPROPERTY_TIMECODE_S&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565781)"><strong>KSPROPERTY_TIMECODE_S</strong></a></p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff568528" data-raw-source="[&lt;strong&gt;TIMECODE_SAMPLE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff568528)"><strong>TIMECODE_SAMPLE</strong></a></p></td>
</tr>
</tbody>
</table>

 

属性值 （操作数据），则时间码\_示例结构，它指定当前磁带位置的绝对跟踪号。

<a name="remarks"></a>备注
-------

**TimecodeSamp** KSPROPERTY 成员\_时间码\_S 结构描述当前磁带位置的绝对跟踪号。

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

[**KSPROPERTY\_TIMECODE\_S**](https://msdn.microsoft.com/library/windows/hardware/ff565781)

[**TIMECODE\_SAMPLE**](https://msdn.microsoft.com/library/windows/hardware/ff568528)

 

 






