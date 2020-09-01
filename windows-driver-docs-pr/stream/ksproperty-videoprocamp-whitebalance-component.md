---
title: KSPROPERTY \_ VIDEOPROCAMP \_ WHITEBALANCE \_ 组件
description: KSPROPERTY \_ VIDEOPROCAMP \_ WHITEBALANCE \_ COMPONENT 属性指定视频格式的蓝和红值中的白平衡设置。
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
ms.openlocfilehash: 2b64a3edae66de42d34e5c1de4fa994ab843131c
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89183955"
---
# <a name="ksproperty_videoprocamp_whitebalance_component"></a>KSPROPERTY \_ VIDEOPROCAMP \_ WHITEBALANCE \_ 组件


KSPROPERTY \_ VIDEOPROCAMP \_ WHITEBALANCE \_ COMPONENT 属性指定视频格式的蓝和红值中的白平衡设置。

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
<td><p>节点</p></td>
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videoprocamp_node_s2" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOPROCAMP_NODE_S2&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videoprocamp_node_s2)"><strong>KSPROPERTY_VIDEOPROCAMP_NODE_S2</strong></a></td>
<td><p>长整数对</p></td>
</tr>
</tbody>
</table>

 

 (操作数据) 的属性值是一对长整数，用于指定相机白平衡设置的红色和蓝色分量。 值指示照相机当前的红色和蓝色分量值。

<a name="remarks"></a>备注
-------

白平衡组件支持的范围和默认值是依赖于实现的。

发出集请求时，客户端应提供**Value1**成员的红色分量值和 KSPROPERTY **Value2** \_ VIDEOPROCAMP \_ 节点 S2 结构的 Value2 成员中的蓝色分量值 \_ 。

若要确定设备支持的白平衡值的范围，应用程序可以发出 KSPROPERTY \_ 类型 \_ BASICSUPPORT 请求。 可以 \_ \_ 在[**KSPROPERTY \_ 项**](/windows-hardware/drivers/ddi/ks/ns-ks-ksproperty_item)结构的**Flags**成员中指定 KSPROPERTY 类型 BASICSUPPORT。

发出 get 请求时，客户端将接收**Value1**成员的红色值和 KSPROPERTY **Value2** \_ VIDEOPROCAMP \_ 节点 S2 结构的 Value2 成员中的蓝色分量值 \_ 。

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

[**KSPROPERTY \_ VIDEOPROCAMP \_ 节点 \_ S2**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videoprocamp_node_s2)

 

