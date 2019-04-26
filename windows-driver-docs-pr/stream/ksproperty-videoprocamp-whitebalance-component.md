---
title: KSPROPERTY\_VIDEOPROCAMP\_WHITEBALANCE\_组件
description: KSPROPERTY\_VIDEOPROCAMP\_WHITEBALANCE\_组件属性的视频格式的蓝色和红色值中指定的白平衡设置。
ms.assetid: ed5faffa-7e31-47ac-bf11-2201d616c6aa
keywords:
- KSPROPERTY_VIDEOPROCAMP_WHITEBALANCE_COMPONENT 流式处理媒体设备
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
ms.openlocfilehash: 5287d0e0f4808813792f9688946a5256a9ed5c60
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327221"
---
# <a name="kspropertyvideoprocampwhitebalancecomponent"></a>KSPROPERTY\_VIDEOPROCAMP\_WHITEBALANCE\_组件


KSPROPERTY\_VIDEOPROCAMP\_WHITEBALANCE\_组件属性的视频格式的蓝色和红色值中指定的白平衡设置。

## <span id="ddk_ksproperty_videoprocamp_whitebalance_component_ks"></span><span id="DDK_KSPROPERTY_VIDEOPROCAMP_WHITEBALANCE_COMPONENT_KS"></span>


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
<td><p>节点</p></td>
<td><a href="https://msdn.microsoft.com/library/windows/hardware/ff566082" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOPROCAMP_NODE_S2&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566082)"><strong>KSPROPERTY_VIDEOPROCAMP_NODE_S2</strong></a></td>
<td><p>对长整数</p></td>
</tr>
</tbody>
</table>

 

属性值 （操作数据） 是长整数，用于指定照相机的白平衡设置红色和蓝色分量的对。 这些值表示照相机的当前红色和蓝色分量值。

<a name="remarks"></a>备注
-------

支持的范围和白平衡组件的默认值是依赖于实现的。

在 set 请求时，客户端应提供中的红色组件值**Value1**中的成员和蓝色分量值**Value2** KSPROPERTY 成员\_VIDEOPROCAMP\_节点\_S2 结构。

若要确定设备支持的白平衡值的范围，应用程序可以发出 KSPROPERTY\_类型\_BASICSUPPORT 请求。 您可以指定 KSPROPERTY\_类型\_中的 BASICSUPPORT**标志**的成员[ **KSPROPERTY\_项**](https://msdn.microsoft.com/library/windows/hardware/ff565176)结构。

客户端时发出 get 请求，接收中的红色值**Value1**中的成员和蓝色分量值**Value2** KSPROPERTY 成员\_VIDEOPROCAMP\_节点\_S2 结构。

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

## <a name="see-also"></a>请参阅


[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)

[**KSPROPERTY\_VIDEOPROCAMP\_NODE\_S2**](https://msdn.microsoft.com/library/windows/hardware/ff566082)

 

 






