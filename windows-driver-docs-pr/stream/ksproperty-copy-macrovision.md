---
title: KSPROPERTY\_COPY\_MACROVISION
description: KSPROPERTY\_COPY\_MACROVISION 属性指示数据流的 Macrovision 级别。
ms.assetid: 6863bcf6-06bc-4bd2-896e-43c083aa07d5
keywords:
- KSPROPERTY_COPY_MACROVISION 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_COPY_MACROVISION
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: fc20a81b063e1680f9fc701776720a7baa3aaafe
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72826774"
---
# <a name="ksproperty_copy_macrovision"></a>KSPROPERTY\_COPY\_MACROVISION


KSPROPERTY\_COPY\_MACROVISION 属性指示数据流的 Macrovision 级别。

## <span id="ddk_ksproperty_copy_macrovision_ks"></span><span id="DDK_KSPROPERTY_COPY_MACROVISION_KS"></span>


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
<td><p>无</p></td>
<td><p>“是”</p></td>
<td><p>大头针</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ks_copy_macrovision" data-raw-source="[&lt;strong&gt;KS_COPY_MACROVISION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ks_copy_macrovision)"><strong>KS_COPY_MACROVISION</strong></a></p></td>
</tr>
</tbody>
</table>

 

属性值（操作数据）是一个 KS\_复制\_MACROVISION 结构，该结构指定数据流的 Macrovision 级别。

<a name="remarks"></a>备注
-------

有关 Macrovision 级别的详细信息，请参阅[DVD 版权保护](https://docs.microsoft.com/windows-hardware/drivers/stream/dvd-copyright-protection)。

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


[**KS\_复制\_MACROVISION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ks_copy_macrovision)

 

 






