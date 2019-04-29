---
title: KSPROPERTY\_STREAM\_PRESENTATIONEXTENT
description: 客户端发送 KSPROPERTY\_流\_PRESENTATIONEXTENT 请求来查询的流范围。
ms.assetid: 36b66035-f935-4264-8555-d949865d708e
keywords:
- KSPROPERTY_STREAM_PRESENTATIONEXTENT 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_STREAM_PRESENTATIONEXTENT
api_location:
- ks.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7c6eafdaf4c0d7e10e9a9f7700e0a50c49e1bae7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63324225"
---
# <a name="kspropertystreampresentationextent"></a>KSPROPERTY\_STREAM\_PRESENTATIONEXTENT


客户端发送 KSPROPERTY\_流\_PRESENTATIONEXTENT 请求来查询的流范围。

## <span id="ddk_ksproperty_stream_presentationextent_ks"></span><span id="DDK_KSPROPERTY_STREAM_PRESENTATIONEXTENT_KS"></span>


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
<td><p>LONGLONG</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

属性返回作为 LONGLONG，使用相同的分辨率格式作为呈现时间范围。

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
<td>Ks.h （包括 Ks.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)

 

 






