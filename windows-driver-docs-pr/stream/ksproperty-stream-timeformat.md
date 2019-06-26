---
title: KSPROPERTY\_STREAM\_TIMEFORMAT
description: KSPROPERTY\_流\_TIMEFORMAT 属性用于检索特定 pin 连接上使用的时间格式。
ms.assetid: bf8c32b2-401f-4f89-bcca-97a07c50cc45
keywords:
- KSPROPERTY_STREAM_TIMEFORMAT 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_STREAM_TIMEFORMAT
api_location:
- ks.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c66ce9b849197e58e4a9a1c3457d85a4916ef423
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368841"
---
# <a name="kspropertystreamtimeformat"></a>KSPROPERTY\_STREAM\_TIMEFORMAT


KSPROPERTY\_流\_TIMEFORMAT 属性用于检索特定 pin 连接上使用的时间格式。

## <span id="ddk_ksproperty_stream_timeformat_ks"></span><span id="DDK_KSPROPERTY_STREAM_TIMEFORMAT_KS"></span>


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
<td><p>GUID</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

该属性返回指定在连接中使用和指示格式的呈现时间和范围的时间格式的 GUID。 定义的时间格式对应于由 DirectShow 定义。

KSPROPERTY\_流\_TIMEFORMAT 是可选属性，如果 pin 支持率、 演示文稿时间/范围内，应实现或跳过下降属性 (有关这些属性的详细信息，请参阅[质量管理](https://docs.microsoft.com/windows-hardware/drivers/stream/quality-management))。 这允许客户端确定用来连接和速率、 演示文稿时间/范围内，使用时间戳信息的格式的时间格式，并跳过降级操作。

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

 

 






