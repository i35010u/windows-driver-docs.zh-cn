---
title: KSPROPERTY \_ VIDEOPROCAMP \_ 数字 \_ 乘数
description: KSPROPERTY \_ VIDEOPROCAMP \_ 数字 \_ 乘数属性指定要应用于图像的数字缩放量。
keywords:
- KSPROPERTY_VIDEOPROCAMP_DIGITAL_MULTIPLIER 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_VIDEOPROCAMP_DIGITAL_MULTIPLIER
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9df1472f4d4ff8a697332dad0d0a9641ae3da3f5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840239"
---
# <a name="ksproperty_videoprocamp_digital_multiplier"></a>KSPROPERTY \_ VIDEOPROCAMP \_ 数字 \_ 乘数


KSPROPERTY \_ VIDEOPROCAMP \_ 数字 \_ 乘数属性指定要应用于图像的数字缩放量。

## <span id="ddk_ksproperty_videoprocamp_digital_multiplier_ks"></span><span id="DDK_KSPROPERTY_VIDEOPROCAMP_DIGITAL_MULTIPLIER_KS"></span>


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

 

) 操作数据 (的属性值是指定相机的数字乘数设置的 LONG。 值指定相机应用于图像的数字乘数值。

<a name="remarks"></a>备注
-------

发出集请求时，客户端应提供 KSPROPERTY VIDEOPROCAMP 节点的 **值** 成员的数字乘数值 \_ \_ \_ 。

若要确定设备支持的数字乘数的范围，应用程序可以发出 KSPROPERTY \_ 类型 \_ BASICSUPPORT 请求。 可以 \_ \_ 在 [**KSPROPERTY \_ 项**](/windows-hardware/drivers/ddi/ks/ns-ks-ksproperty_item)结构的 **Flags** 成员中指定 KSPROPERTY 类型 BASICSUPPORT。

发出 get 请求时，客户端将在 KSPROPERTY VIDEOPROCAMP 节点的结构的 **值** 成员中接收 LONG 类型的值 \_ \_ \_ 。

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

## <a name="see-also"></a>请参阅


[**KSPROPERTY**](/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)

[**KSPROPERTY \_ VIDEOPROCAMP \_ S**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videoprocamp_s)

