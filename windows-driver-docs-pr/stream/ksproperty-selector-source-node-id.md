---
title: KSPROPERTY\_选择器\_源\_节点\_ID
description: KSPROPERTY\_选择器\_源\_节点\_ID 属性指定特定节点的源 pin 的 pin 标识符。
ms.assetid: 7616e834-462c-4e2c-8a4f-ec20db042e3b
keywords:
- KSPROPERTY_SELECTOR_SOURCE_NODE_ID 流媒体设备
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
ms.openlocfilehash: 42196b96be48dd3880b82df8e84916b7d53cecf6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838829"
---
# <a name="ksproperty_selector_source_node_id"></a>KSPROPERTY\_选择器\_源\_节点\_ID


KSPROPERTY\_选择器\_源\_节点\_ID 属性指定特定节点的源 pin 的 pin 标识符。

## <span id="ddk_ksproperty_selector_source_node_id_ks"></span><span id="DDK_KSPROPERTY_SELECTOR_SOURCE_NODE_ID_KS"></span>


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
<td><p>“是”</p></td>
<td><p>“是”</p></td>
<td><p>筛选器或节点</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_selector_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_SELECTOR_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_selector_s)"><strong>KSPROPERTY_SELECTOR_S</strong></a>或<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_selector_node_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_SELECTOR_NODE_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_selector_node_s)"> <strong>KSPROPERTY_SELECTOR_NODE_S</strong></a></p></td>
<td><p>漫长</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

发出集请求时，客户端必须在属性描述符结构的**值**成员中指定有效的 pin 标识符。

发出 get 请求时，客户端将接收属性说明符结构的**值**成员中的 pin 标识符。

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

 

 





