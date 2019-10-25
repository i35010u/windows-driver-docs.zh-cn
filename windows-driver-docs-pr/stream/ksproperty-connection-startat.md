---
title: KSPROPERTY\_连接\_STARTAT
description: KSPROPERTY\_连接\_STARTAT 是一个可选属性，该属性由支持在指定事件发生时启动的筛选器实现。
ms.assetid: fcf76316-4016-4218-8530-5ef79794769a
keywords:
- KSPROPERTY_CONNECTION_STARTAT 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_CONNECTION_STARTAT
api_location:
- ks.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 67d6752a4452298f3ff0ca3a81951c6d63e67954
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72826781"
---
# <a name="ksproperty_connection_startat"></a>KSPROPERTY\_连接\_STARTAT


KSPROPERTY\_连接\_STARTAT 是一个可选属性，该属性由支持在指定事件发生时启动的筛选器实现。

## <span id="ddk_ksproperty_connection_startat_ks"></span><span id="DDK_KSPROPERTY_CONNECTION_STARTAT_KS"></span>


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
<td><p>Filter</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksrelativeevent" data-raw-source="[&lt;strong&gt;KSRELATIVEEVENT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksrelativeevent)"><strong>KSRELATIVEEVENT</strong></a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

仅当 pin 处于暂停状态时，才应请求此属性，以将 pin 转换为运行状态。

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
<td>Ks （包含 Ks）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**KSRELATIVEEVENT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksrelativeevent)

[**KSEVENT\_项**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksevent_item)

 

 






