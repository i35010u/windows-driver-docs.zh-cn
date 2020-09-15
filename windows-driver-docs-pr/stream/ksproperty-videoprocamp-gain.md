---
title: KSPROPERTY \_ VIDEOPROCAMP \_ 增益
description: KSPROPERTY \_ VIDEOPROCAMP \_ 增益属性设置或获取相机增益。 此属性是可选的。
ms.assetid: 46ed6ba1-1413-4466-9125-2d0a3fd51def
keywords:
- KSPROPERTY_VIDEOPROCAMP_GAIN 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_VIDEOPROCAMP_GAIN
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7f767b59a20b5f4d8c986342a9eceec4577c3c03
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90103990"
---
# <a name="ksproperty_videoprocamp_gain"></a>KSPROPERTY \_ VIDEOPROCAMP \_ 增益


KSPROPERTY \_ VIDEOPROCAMP \_ 增益属性设置或获取相机增益。 此属性是可选的。

## <span id="ddk_ksproperty_videoprocamp_gain_ks"></span><span id="DDK_KSPROPERTY_VIDEOPROCAMP_GAIN_KS"></span>


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
<td><p>是</p></td>
<td><p>筛选器或节点</p></td>
<td><p><a href="/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videoprocamp_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOPROCAMP_S&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videoprocamp_s)"><strong>KSPROPERTY_VIDEOPROCAMP_S</strong></a>或<a href="/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videoprocamp_node_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOPROCAMP_NODE_S&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videoprocamp_node_s)"> <strong>KSPROPERTY_VIDEOPROCAMP_NODE_S</strong></a></p></td>
<td><p>LONG</p></td>
</tr>
</tbody>
</table>

 

 (操作数据) 的属性值是指定相机增益设置的 LONG 值。

<a name="remarks"></a>备注
-------

KSPROPERTY **Value** \_ VIDEOPROCAMP S 结构的值成员 \_ 指定请求的或当前增益，具体取决于此请求是*get*还是*Set*请求。

收益范围是由供应商定义的;默认分辨率为1。

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
<td>Ksmedia (包含 Ksmedia) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**KSPROPERTY**](/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)

[**KSPROPERTY \_ VIDEOPROCAMP \_ S**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videoprocamp_s)

[**KSPROPERTY \_ VIDEOPROCAMP \_ 节点 \_ S**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videoprocamp_node_s)

