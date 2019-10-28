---
title: KSPROPERTY\_CAMERACONTROL\_PANTILT\_相对
description: KSPROPERTY\_CAMERACONTROL\_PANTILT\_相对属性指定相机的水平或垂直旋转，并可同时指定两者。
ms.assetid: c2c9405c-7713-439f-a150-51969a2a5e6b
keywords:
- KSPROPERTY_CAMERACONTROL_PANTILT_RELATIVE 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_PANTILT_RELATIVE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 227c13b5ad520bcd839843748076b0ea5cc45c72
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843344"
---
# <a name="ksproperty_cameracontrol_pantilt_relative"></a>KSPROPERTY\_CAMERACONTROL\_PANTILT\_相对


KSPROPERTY\_CAMERACONTROL\_PANTILT\_相对属性指定相机的水平或垂直旋转，并可同时指定两者。

## <span id="ddk_ksproperty_cameracontrol_pantilt_relative_ks"></span><span id="DDK_KSPROPERTY_CAMERACONTROL_PANTILT_RELATIVE_KS"></span>


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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_node_s2" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_NODE_S2&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_node_s2)"><strong>KSPROPERTY_CAMERACONTROL_NODE_S2</strong></a>或<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_s2" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_S2&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_s2)"><strong>KSPROPERTY_CAMERACONTROL_S2</strong></a> ，具体取决于请求是用于筛选器还是节点</p></td>
<td><p>长整数对</p></td>
</tr>
</tbody>
</table>

 

属性值（操作数据）是一对长整数，用于指定相机的相对平移和倾斜设置。 值的大小表示所需的平移速度;较高的值表示较高的速度。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>value1</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>0</p></td>
<td><p>停止照相机的水平运动。</p></td>
</tr>
<tr class="even">
<td><p>正值</p></td>
<td><p>开始平移。</p></td>
</tr>
<tr class="odd">
<td><p>负值</p></td>
<td><p>开始平移。</p></td>
</tr>
</tbody>
</table>

 

值的大小表示所需的倾斜速度;较高的值表示较高的速度。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Value2</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>0</p></td>
<td><p>停止照相机的垂直运动。</p></td>
</tr>
<tr class="even">
<td><p>正值</p></td>
<td><p>开始旋转摄像机。</p></td>
</tr>
<tr class="odd">
<td><p>负值</p></td>
<td><p>开始向下旋转相机。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

发出用于平移照相机的 set 请求时，客户端应在属性描述符结构的**Value1**成员的上表中提供其中一个值。

同样，在发出用于倾斜照相机的集的请求时，客户端将提供属性说明符结构的**Value2**成员的上表中的值之一。

发出 get 请求时，客户端将接收**Value1**成员中的平移值和 KSPROPERTY\_CAMERACONTROL 的**Value2**成员中的斜度值，\_S2 或 KSPROPERTY\_CAMERACONTROL\_节点\_s2构造. 值指示相机的当前平移或倾斜状态。

请注意，特定设备可能仅支持特定的速度范围。 若要确定设备支持的速度范围，应用程序可以\_BASICSUPPORT 请求发出 KSPROPERTY\_类型。 可以在[**KSPROPERTY\_项**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksproperty_item)结构的**Flags**成员中指定 KSPROPERTY\_类型\_BASICSUPPORT。

某些设备只支持单一平移或倾斜速度。 在这种情况下， **Value1**或**Value2**成员的符号指示平移方向。

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
<td><p>标头</p></td>
<td>Ksmedia （包括 Ksmedia）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**KSPROPERTY\_CAMERACONTROL\_S2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_s2)

[**KSPROPERTY\_CAMERACONTROL\_NODE\_S2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_node_s2)

 

 






