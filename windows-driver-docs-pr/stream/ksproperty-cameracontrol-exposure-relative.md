---
title: KSPROPERTY\_CAMERACONTROL\_暴露\_相对
description: KSPROPERTY\_CAMERACONTROL\_暴露\_相对属性指定的电子快门速度。
ms.assetid: a4003fcd-9dc8-4889-9ce0-e4f09273d152
keywords:
- KSPROPERTY_CAMERACONTROL_EXPOSURE_RELATIVE 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_EXPOSURE_RELATIVE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3bbd9c5d99a45299554a2b4684d354f6bb27c14f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331695"
---
# <a name="kspropertycameracontrolexposurerelative"></a>KSPROPERTY\_CAMERACONTROL\_暴露\_相对


KSPROPERTY\_CAMERACONTROL\_暴露\_相对属性指定的电子快门速度。

## <span id="ddk_ksproperty_cameracontrol_exposure_relative_ks"></span><span id="DDK_KSPROPERTY_CAMERACONTROL_EXPOSURE_RELATIVE_KS"></span>


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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564439" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_S&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564439)"><strong>KSPROPERTY_CAMERACONTROL_S</strong> </a>或<a href="https://msdn.microsoft.com/library/windows/hardware/ff564420" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_NODE_S&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564420)"> <strong>KSPROPERTY_CAMERACONTROL_NODE_S</strong></a></p></td>
<td><p>长</p></td>
</tr>
</tbody>
</table>

 

属性值 （操作数据） 为指定照相机的相对风险设置长时间。 步骤大小与硬件相关。 若要确定步骤大小，可以发出 get 请求上[ **KSPROPERTY\_CAMERACONTROL\_暴露**](ksproperty-cameracontrol-exposure.md)属性。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>值</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>0</p></td>
<td><p>设置为特定于实现的默认值的暴露时间。</p></td>
</tr>
<tr class="even">
<td><p>正值</p></td>
<td><p>通过一个步骤中增加的暴露时间。</p></td>
</tr>
<tr class="odd">
<td><p>负值</p></td>
<td><p>递减一个步骤的暴露时间。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

在 set 请求时，应提供在上表中的值之一**值**KSPROPERTY 成员\_CAMERACONTROL\_节点\_S 结构。

时发出 get 请求，客户端接收的值之一在上表中的值成员的 KSPROPERTY\_CAMERACONTROL\_节点\_S 结构。 值指示用于相机的当前暴露时间设置。

如果自动公开模式控制是在 Auto 模式或 Aperture 优先级模式下，设置请求将失败。

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


[**KSPROPERTY\_CAMERACONTROL\_节点\_S**](https://msdn.microsoft.com/library/windows/hardware/ff564420)

 

 






