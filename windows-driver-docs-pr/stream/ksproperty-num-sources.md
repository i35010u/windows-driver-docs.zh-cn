---
title: KSPROPERTY\_NUM\_源
description: KSPROPERTY\_NUM\_源属性指定选择器单元上的输入插针数目。
ms.assetid: 94d0f926-0551-4fe2-aa7f-2898e04c4b36
keywords:
- KSPROPERTY_NUM_SOURCES 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_NUM_SOURCES
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8973dc2fe5519036dc3fb3bdb4d6ef312bfb3099
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842753"
---
# <a name="ksproperty_num_sources"></a>KSPROPERTY\_NUM\_源


KSPROPERTY\_NUM\_源属性指定选择器单元上的输入插针数目。

## <span id="ddk_ksproperty_num_sources_ks"></span><span id="DDK_KSPROPERTY_NUM_SOURCES_KS"></span>


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
<td><p>无</p></td>
<td><p>筛选器或节点</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_selector_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_SELECTOR_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_selector_s)"><strong>KSPROPERTY_SELECTOR_S</strong></a>或<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_selector_node_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_SELECTOR_NODE_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_selector_node_s)"> <strong>KSPROPERTY_SELECTOR_NODE_S</strong></a></p></td>
<td><p>漫长</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

发出 get 请求时，客户端将接收属性说明符结构的**值**成员中可用源的数目。

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

 

 





