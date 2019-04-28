---
title: KSPROPERTY\_CAMERACONTROL\_焦点\_长度
description: KSPROPERTY\_CAMERACONTROL\_焦点\_长度属性检索用于相机的焦点长度信息。
ms.assetid: a7fba5e4-abd1-46ae-b93c-5fede0249771
keywords:
- KSPROPERTY_CAMERACONTROL_FOCAL_LENGTH 流式处理媒体设备
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
ms.openlocfilehash: 5512d79baa88e74de9a386e36fdd11b614781fa8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63341829"
---
# <a name="kspropertycameracontrolfocallength"></a>KSPROPERTY\_CAMERACONTROL\_焦点\_长度


KSPROPERTY\_CAMERACONTROL\_焦点\_长度属性检索用于相机的焦点长度信息。

## <span id="ddk_ksproperty_cameracontrol_focal_length_ks"></span><span id="DDK_KSPROPERTY_CAMERACONTROL_FOCAL_LENGTH_KS"></span>


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
<td><p>否</p></td>
<td><p>筛选器或节点</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564408" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_FOCAL_LENGTH_S&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564408)"><strong>KSPROPERTY_CAMERACONTROL_FOCAL_LENGTH_S</strong> </a>或<a href="https://msdn.microsoft.com/library/windows/hardware/ff564418" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_NODE_FOCAL_LENGTH_S&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564418)"> <strong>KSPROPERTY_CAMERACONTROL_NODE_FOCAL_LENGTH_S</strong></a></p></td>
<td><p>长</p></td>
</tr>
</tbody>
</table>

 

属性值 （操作数据） 为指定照相机的焦点长度长时间。

<a name="remarks"></a>备注
-------

您可以使用此属性请求解释缩放值。 缩放的范围应介于**lObjectiveFocalLengthMin**/**lOcularFocalLength**并**lObjectiveFocalLengthMax** / **lOcularFocalLength**。 (**lOcularFocalLength**， **lObjectiveFocalLengthMin**，并**lObjectiveFocalLengthMax**属于[ **KSPROPERTY\_CAMERACONTROL\_焦点\_长度\_S** ](https://msdn.microsoft.com/library/windows/hardware/ff564408)并[ **KSPROPERTY\_CAMERACONTROL\_节点\_焦\_长度\_S** ](https://msdn.microsoft.com/library/windows/hardware/ff564418)结构。)

例如，如果**lObjectiveFocalLengthMax** = 105 和**lOcularFocalLength** = 35，则此照相机是支持的最大视觉缩放比率为 105/35 或 3。

另请参阅*光学缩放*USB 视频类设备类规范的节。 此规范位于[USB 实现论坛](https://go.microsoft.com/fwlink/p/?linkid=8780)网站。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Version</p></td>
<td><p>适用于 Windows Vista 和更高版本的 Windows 操作系统。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ksmedia.h （包括 Ksmedia.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**KSPROPERTY\_CAMERACONTROL\_焦点\_长度\_S**](https://msdn.microsoft.com/library/windows/hardware/ff564408)

[**KSPROPERTY\_CAMERACONTROL\_节点\_焦点\_长度\_S**](https://msdn.microsoft.com/library/windows/hardware/ff564418)

[**KSPROPERTY\_CAMERACONTROL\_ZOOM**](ksproperty-cameracontrol-zoom.md)

[**KSPROPERTY\_CAMERACONTROL\_ZOOM\_RELATIVE**](ksproperty-cameracontrol-zoom-relative.md)

 

 






