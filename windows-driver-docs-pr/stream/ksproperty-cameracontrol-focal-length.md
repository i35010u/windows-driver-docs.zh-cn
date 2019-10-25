---
title: KSPROPERTY\_CAMERACONTROL\_焦\_长度
description: KSPROPERTY\_CAMERACONTROL\_焦\_LENGTH 属性检索照相机的焦距信息。
ms.assetid: a7fba5e4-abd1-46ae-b93c-5fede0249771
keywords:
- KSPROPERTY_CAMERACONTROL_FOCAL_LENGTH 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_FOCAL_LENGTH
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 28eef3519d1cf657f2a1e239a7aa00d8be8098d0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840466"
---
# <a name="ksproperty_cameracontrol_focal_length"></a>KSPROPERTY\_CAMERACONTROL\_焦\_长度


KSPROPERTY\_CAMERACONTROL\_焦\_LENGTH 属性检索照相机的焦距信息。

## <span id="ddk_ksproperty_cameracontrol_focal_length_ks"></span><span id="DDK_KSPROPERTY_CAMERACONTROL_FOCAL_LENGTH_KS"></span>


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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_focal_length_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_FOCAL_LENGTH_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_focal_length_s)"><strong>KSPROPERTY_CAMERACONTROL_FOCAL_LENGTH_S</strong></a>或<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_node_focal_length_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_NODE_FOCAL_LENGTH_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_node_focal_length_s)"> <strong>KSPROPERTY_CAMERACONTROL_NODE_FOCAL_LENGTH_S</strong></a></p></td>
<td><p>漫长</p></td>
</tr>
</tbody>
</table>

 

属性值（操作数据）是指定相机焦距的 LONG。

<a name="remarks"></a>备注
-------

您可以使用此属性请求来解释缩放值。 缩放范围应介于**lObjectiveFocalLengthMin**/**lOcularFocalLength**和**lObjectiveFocalLengthMax**/**lOcularFocalLength**之间。 （**lOcularFocalLength**、 **lObjectiveFocalLengthMin**和**lObjectiveFocalLengthMax**是[**KSPROPERTY\_CAMERACONTROL\_焦\_长度\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_focal_length_s)和 KSPROPERTY 的成员[ **\_CAMERACONTROL\_节点\_焦\_长度\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_node_focal_length_s)结构。）

例如，如果**lObjectiveFocalLengthMax** = 105， **lOcularFocalLength** = 35，则此照相机的最大视觉缩放比率为105/35，即为3。

另请参阅 USB 视频类设备类规范的 "*光学缩放*" 部分。 此规范可在[USB 实现论坛](https://go.microsoft.com/fwlink/p/?linkid=8780)网站上找到。

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


[**KSPROPERTY\_CAMERACONTROL\_焦\_长度\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_focal_length_s)

[**KSPROPERTY\_CAMERACONTROL\_NODE\_焦\_长度\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_node_focal_length_s)

[**KSPROPERTY\_CAMERACONTROL\_缩放**](ksproperty-cameracontrol-zoom.md)

[**KSPROPERTY\_CAMERACONTROL\_缩放\_相对**](ksproperty-cameracontrol-zoom-relative.md)

 

 






