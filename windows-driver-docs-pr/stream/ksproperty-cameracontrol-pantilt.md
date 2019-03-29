---
title: KSPROPERTY\_CAMERACONTROL\_PANTILT
description: KSPROPERTY\_CAMERACONTROL\_PANTILT 属性指定绝对平移和倾斜设置。
ms.assetid: d6f151c9-a428-4d76-9854-5064d901643e
keywords:
- KSPROPERTY_CAMERACONTROL_PANTILT 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_PANTILT
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: fe1fa9526e25ac23f8c3df2dea5d6d7b7535d053
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566589"
---
# <a name="kspropertycameracontrolpantilt"></a>KSPROPERTY\_CAMERACONTROL\_PANTILT


KSPROPERTY\_CAMERACONTROL\_PANTILT 属性指定绝对平移和倾斜设置。

## <span id="ddk_ksproperty_cameracontrol_pantilt_ks"></span><span id="DDK_KSPROPERTY_CAMERACONTROL_PANTILT_KS"></span>


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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564451" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_S2&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564451)"><strong>KSPROPERTY_CAMERACONTROL_S2</strong> </a>或<a href="https://msdn.microsoft.com/library/windows/hardware/ff564421" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_NODE_S2&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564421)"> <strong>KSPROPERTY_CAMERACONTROL_NODE_S2</strong> </a>具体取决于该请求是一个筛选器或节点</p></td>
<td><p>对长整数</p></td>
</tr>
</tbody>
</table>

 

属性值 （操作数据） 是一对指定照相机的绝对平移和倾斜设置的长整数。 这些值表示弧线秒为单位。

一个弧第二个是在某种程度上的 1/3600。 可接受的值范围从 −180\*3600 到 + 180\*3600 弧度秒。 如果未提供为平移或倾斜的值，默认值为 0。

平移请求时，指定旋转照相机传送到右侧，并指定负数值来旋转照相机传送到左侧是正数值。

正值倾斜请求时，将向上倾斜照相机和负数值向下倾斜照相机。

<a name="remarks"></a>备注
-------

**Value1**的成员[ **KSPROPERTY\_CAMERACONTROL\_S2** ](https://msdn.microsoft.com/library/windows/hardware/ff564451)或[ **KSPROPERTY\_CAMERACONTROL\_节点\_S2** ](https://msdn.microsoft.com/library/windows/hardware/ff564421)结构指定的平移设置。 **Value2**成员指定倾斜设置。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>版本</p></td>
<td><p>适用于 Windows Vista 和更高版本的 Windows 操作系统。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ksmedia.h （包括 Ksmedia.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**KSPROPERTY\_CAMERACONTROL\_S2**](https://msdn.microsoft.com/library/windows/hardware/ff564451)

[**KSPROPERTY\_CAMERACONTROL\_节点\_S2**](https://msdn.microsoft.com/library/windows/hardware/ff564421)

 

 






