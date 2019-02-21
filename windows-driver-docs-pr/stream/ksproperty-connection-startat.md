---
title: KSPROPERTY\_连接\_STARTAT
description: KSPROPERTY\_连接\_STARTAT 是由支持指定的事件发生时启动的筛选器实现的可选属性。
ms.assetid: fcf76316-4016-4218-8530-5ef79794769a
keywords:
- KSPROPERTY_CONNECTION_STARTAT 流式处理媒体设备
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
ms.openlocfilehash: 0d20d6da973b5a5a49bd7f0e5bf7c24adee375c0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543618"
---
# <a name="kspropertyconnectionstartat"></a>KSPROPERTY\_连接\_STARTAT


KSPROPERTY\_连接\_STARTAT 是由支持指定的事件发生时启动的筛选器实现的可选属性。

## <span id="ddk_ksproperty_connection_startat_ks"></span><span id="DDK_KSPROPERTY_CONNECTION_STARTAT_KS"></span>


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
<td><p>否</p></td>
<td><p>是</p></td>
<td><p>Filter</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566776" data-raw-source="[&lt;strong&gt;KSRELATIVEEVENT&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566776)"><strong>KSRELATIVEEVENT</strong></a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

Pin 处于暂停状态，若要转换到运行状态的 pin 时，应仅请求此属性。

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
<td>Ks.h （包括 Ks.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**KSRELATIVEEVENT**](https://msdn.microsoft.com/library/windows/hardware/ff566776)

[**KSEVENT\_ITEM**](https://msdn.microsoft.com/library/windows/hardware/ff561862)

 

 






