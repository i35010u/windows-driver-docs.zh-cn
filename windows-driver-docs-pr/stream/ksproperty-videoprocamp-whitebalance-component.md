---
title: KSPROPERTY\_VIDEOPROCAMP\_WHITEBALANCE\_组件
description: KSPROPERTY\_VIDEOPROCAMP\_WHITEBALANCE\_组件属性指定视频格式的白平衡设置（蓝色）和红色值。
ms.assetid: ed5faffa-7e31-47ac-bf11-2201d616c6aa
keywords:
- KSPROPERTY_VIDEOPROCAMP_WHITEBALANCE_COMPONENT 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_VIDEOPROCAMP_WHITEBALANCE_COMPONENT
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c8d911dfa6aca6b42c1163bb65f0eba3cbcf94b0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842821"
---
# <a name="ksproperty_videoprocamp_whitebalance_component"></a>KSPROPERTY\_VIDEOPROCAMP\_WHITEBALANCE\_组件


KSPROPERTY\_VIDEOPROCAMP\_WHITEBALANCE\_组件属性指定视频格式的白平衡设置（蓝色）和红色值。

## <span id="ddk_ksproperty_videoprocamp_whitebalance_component_ks"></span><span id="DDK_KSPROPERTY_VIDEOPROCAMP_WHITEBALANCE_COMPONENT_KS"></span>


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
<td><p>节点</p></td>
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videoprocamp_node_s2" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOPROCAMP_NODE_S2&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videoprocamp_node_s2)"><strong>KSPROPERTY_VIDEOPROCAMP_NODE_S2</strong></a></td>
<td><p>长整数对</p></td>
</tr>
</tbody>
</table>

 

属性值（操作数据）是一对长整数，用于指定相机白平衡设置的红色和蓝色分量。 值指示照相机当前的红色和蓝色分量值。

<a name="remarks"></a>备注
-------

白平衡组件支持的范围和默认值是依赖于实现的。

发出集请求时，客户端应在**Value1**成员中提供红色分量值，并在 KSPROPERTY\_VIDEOPROCAMP\_节点的**Value2**成员中提供蓝色分量值\_S2 结构。

若要确定设备支持的白平衡值的范围，应用程序可以\_BASICSUPPORT 请求发出 KSPROPERTY\_类型。 可以在[**KSPROPERTY\_项**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksproperty_item)结构的**Flags**成员中指定 KSPROPERTY\_类型\_BASICSUPPORT。

发出 get 请求时，客户端将接收**Value1**成员的红色值和 KSPROPERTY\_VIDEOPROCAMP\_节点的**Value2**成员中的蓝色分量值\_S2 结构。

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


[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)

[**KSPROPERTY\_VIDEOPROCAMP\_NODE\_S2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videoprocamp_node_s2)

 

 






