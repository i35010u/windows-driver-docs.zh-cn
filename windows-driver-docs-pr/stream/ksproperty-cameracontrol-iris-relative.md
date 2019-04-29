---
title: KSPROPERTY\_CAMERACONTROL\_鸢尾花\_相对
description: KSPROPERTY\_CAMERACONTROL\_鸢尾花\_相对属性指定照相机的 aperture 设置。
ms.assetid: 919fcf7a-ee96-4e1e-b0ce-e5a7ce5086c7
keywords:
- KSPROPERTY_CAMERACONTROL_IRIS_RELATIVE 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_IRIS_RELATIVE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c17eebde02f8d0abf782bb3a6f5d012807ac7471
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63363162"
---
# <a name="kspropertycameracontrolirisrelative"></a>KSPROPERTY\_CAMERACONTROL\_鸢尾花\_相对


KSPROPERTY\_CAMERACONTROL\_鸢尾花\_相对属性指定照相机的 aperture 设置。

## <span id="ddk_ksproperty_cameracontrol_iris_relative_ks"></span><span id="DDK_KSPROPERTY_CAMERACONTROL_IRIS_RELATIVE_KS"></span>


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
<td><p>否</p></td>
<td><p>是</p></td>
<td><p>筛选器或节点</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564439" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_S&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564439)"><strong>KSPROPERTY_CAMERACONTROL_S</strong> </a>或<a href="https://msdn.microsoft.com/library/windows/hardware/ff564420" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_NODE_S&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564420)"> <strong>KSPROPERTY_CAMERACONTROL_NODE_S</strong></a></p></td>
<td><p>长</p></td>
</tr>
</tbody>
</table>

 

属性值 （操作数据） 为指定照相机的相对鸢尾花设置长时间。 请注意，鸢尾花步骤大小和鸢尾花步骤默认值是特定于实现的。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>ReplTest1</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>0</p></td>
<td><p>设置为默认打开的鸢尾花。 此默认值为特定于实现的并在硬件中提供。</p></td>
</tr>
<tr class="even">
<td><p>正值</p></td>
<td><p>打开鸢尾花一步。</p></td>
</tr>
<tr class="odd">
<td><p>负值</p></td>
<td><p>关闭鸢尾花一步。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

在 set 请求时，应提供在上表中的值之一**值**KSPROPERTY 成员\_CAMERACONTROL\_节点\_S 结构。

如果自动公开模式控制是在 Auto 模式或快门优先级模式下，设置请求将失败。

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

 

 






