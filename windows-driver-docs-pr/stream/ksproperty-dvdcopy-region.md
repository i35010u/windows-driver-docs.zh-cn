---
title: KSPROPERTY\_DVDCOPY\_区域
description: KSPROPERTY\_DVDCOPY\_REGION 属性指定 DVD 复制保护区域根据语言限制。
ms.assetid: b0ad355b-607f-43c5-9959-a309c6c63259
keywords:
- KSPROPERTY_DVDCOPY_REGION 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_DVDCOPY_REGION
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 53aea7985010841a83d0447ef7cb073ba4c5b018
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63377211"
---
# <a name="kspropertydvdcopyregion"></a>KSPROPERTY\_DVDCOPY\_区域


KSPROPERTY\_DVDCOPY\_REGION 属性指定 DVD 复制保护区域根据语言限制。

## <span id="ddk_ksproperty_dvdcopy_region_ks"></span><span id="DDK_KSPROPERTY_DVDCOPY_REGION_KS"></span>


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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567638" data-raw-source="[&lt;strong&gt;KS_DVDCOPY_REGION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567638)"><strong>KS_DVDCOPY_REGION</strong></a></p></td>
</tr>
</tbody>
</table>

 

属性值 （操作数据） 是 KS\_DVDCOPY\_区域结构描述民族或语言的区域代码。

<a name="remarks"></a>备注
-------

有关语言限制的详细信息，请参阅[DVD 之前实行](https://msdn.microsoft.com/library/windows/hardware/ff559512)并[DVD 版权保护](https://msdn.microsoft.com/library/windows/hardware/ff558736)。

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


[**KS\_DVDCOPY\_REGION**](https://msdn.microsoft.com/library/windows/hardware/ff567638)

 

 






