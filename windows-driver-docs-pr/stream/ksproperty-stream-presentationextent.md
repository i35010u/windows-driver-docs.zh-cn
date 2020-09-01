---
title: KSPROPERTY \_ 流 \_ PRESENTATIONEXTENT
description: 客户端发送 KSPROPERTY \_ stream \_ PRESENTATIONEXTENT 请求来查询流区。
ms.assetid: 36b66035-f935-4264-8555-d949865d708e
keywords:
- KSPROPERTY_STREAM_PRESENTATIONEXTENT 流媒体设备
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
ms.openlocfilehash: 730f36e5ec9d8b3154eb19739d1cfee95500600b
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89189985"
---
# <a name="ksproperty_stream_presentationextent"></a>KSPROPERTY \_ 流 \_ PRESENTATIONEXTENT


客户端发送 KSPROPERTY \_ stream \_ PRESENTATIONEXTENT 请求来查询流区。

## <span id="ddk_ksproperty_stream_presentationextent_ks"></span><span id="DDK_KSPROPERTY_STREAM_PRESENTATIONEXTENT_KS"></span>


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
<th>获取</th>
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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p>LONGLONG</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

属性以 LONGLONG 的形式返回区，其解决格式与显示时间相同。

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
<td>Ks (包含 Ks .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**KSPROPERTY**](/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)

 

