---
title: KSPROPERTY \_ CAMERACONTROL \_ PANTILT
description: KSPROPERTY \_ CAMERACONTROL \_ PANTILT 属性指定绝对平移和倾斜设置。
ms.assetid: d6f151c9-a428-4d76-9854-5064d901643e
keywords:
- KSPROPERTY_CAMERACONTROL_PANTILT 流媒体设备
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
ms.openlocfilehash: 57b6ffde781f9e0420c83f052e32ebe934c71aa0
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89192997"
---
# <a name="ksproperty_cameracontrol_pantilt"></a>KSPROPERTY \_ CAMERACONTROL \_ PANTILT


KSPROPERTY \_ CAMERACONTROL \_ PANTILT 属性指定绝对平移和倾斜设置。

## <span id="ddk_ksproperty_cameracontrol_pantilt_ks"></span><span id="DDK_KSPROPERTY_CAMERACONTROL_PANTILT_KS"></span>


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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_s2" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_S2&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_s2)"><strong>KSPROPERTY_CAMERACONTROL_S2</strong></a> 或 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_node_s2" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_NODE_S2&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_node_s2)"><strong>KSPROPERTY_CAMERACONTROL_NODE_S2</strong></a> ，具体取决于请求是用于筛选器还是节点</p></td>
<td><p>长整数对</p></td>
</tr>
</tbody>
</table>

 

 (操作数据) 的属性值是一对指定相机绝对平移和倾斜设置的长整数。 这些值以弧度/秒单位表示。

一次弧线为1/3600。 可接受的值范围为− 180 \* 3600 到 + 180 \* 3600 弧度秒。 如果未提供平移或倾斜值，则默认值为0。

进行平移请求时，请指定一个正值，使相机向右旋转，并指定一个负值将相机旋转到左侧。

倾斜请求时，正值会向上倾斜摄像机，负值将向下倾斜相机。

<a name="remarks"></a>注解
-------

[**KSPROPERTY \_ CAMERACONTROL \_ s2**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_s2)或[**KSPROPERTY \_ CAMERACONTROL \_ 节点 \_ s2**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_node_s2)结构的**Value1**成员指定平移设置。 **Value2**成员指定倾斜设置。

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
<td><p>适用于 windows Vista 和更高版本的 Windows 操作系统。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ksmedia (包含 Ksmedia) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**KSPROPERTY \_ CAMERACONTROL \_ S2**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_s2)

[**KSPROPERTY \_ CAMERACONTROL \_ 节点 \_ S2**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_node_s2)

 

