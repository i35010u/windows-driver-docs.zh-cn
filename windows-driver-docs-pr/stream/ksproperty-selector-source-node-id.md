---
title: KSPROPERTY\_SELECTOR\_SOURCE\_NODE\_ID
description: KSPROPERTY\_选择器\_源\_节点\_ID 属性指定特定节点的源 pin 的 pin 标识符。
ms.assetid: 7616e834-462c-4e2c-8a4f-ec20db042e3b
keywords:
- KSPROPERTY_SELECTOR_SOURCE_NODE_ID 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_SELECTOR_SOURCE_NODE_ID
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4de90cd85670730df671798de0e5973f6477af69
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376379"
---
# <a name="kspropertyselectorsourcenodeid"></a>KSPROPERTY\_SELECTOR\_SOURCE\_NODE\_ID


KSPROPERTY\_选择器\_源\_节点\_ID 属性指定特定节点的源 pin 的 pin 标识符。

## <span id="ddk_ksproperty_selector_source_node_id_ks"></span><span id="DDK_KSPROPERTY_SELECTOR_SOURCE_NODE_ID_KS"></span>


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
<td><p>是</p></td>
<td><p>筛选器或节点</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_selector_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_SELECTOR_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_selector_s)"><strong>KSPROPERTY_SELECTOR_S</strong> </a>或<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_selector_node_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_SELECTOR_NODE_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_selector_node_s)"> <strong>KSPROPERTY_SELECTOR_NODE_S</strong></a></p></td>
<td><p>长</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

Set 请求时，客户端必须指定一个有效的 pin 标识符**值**属性描述符结构的成员。

在 get 请求时，客户端将接收中的 pin 标识符**值**属性描述符结构的成员。

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

 

 





