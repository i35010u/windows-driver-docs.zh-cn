---
title: KSPROPERTY\_CAMERACONTROL\_缩放
description: 用户模式下客户端使用 KSPROPERTY\_CAMERACONTROL\_缩放属性来获取或设置照相机的缩放设置。 此属性为可选项。
ms.assetid: eceebcee-e7dc-41df-ac44-3b9a9adb0341
keywords:
- KSPROPERTY_CAMERACONTROL_ZOOM 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_ZOOM
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 30e0568011ba9cceba7ee3744f9fdc66c39d8400
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541331"
---
# <a name="kspropertycameracontrolzoom"></a>KSPROPERTY\_CAMERACONTROL\_缩放


用户模式下客户端使用 KSPROPERTY\_CAMERACONTROL\_缩放属性来获取或设置照相机的缩放设置。 此属性为可选项。

## <span id="ddk_ksproperty_cameracontrol_zoom_ks"></span><span id="DDK_KSPROPERTY_CAMERACONTROL_ZOOM_KS"></span>


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

 

属性值 （操作数据） 为 long 类型的值，指定照相机的缩放设置。 此值是以毫米为单位表示。

<a name="remarks"></a>备注
-------

**值**KSPROPERTY 成员\_CAMERACONTROL\_S 结构指定的缩放。

每个视频捕获微型驱动程序支持此属性必须定义此属性的范围和默认值。 设备的范围必须是 10 到 600。 默认值必须为 10。

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
<td>Ksmedia.h （包括 Ksmedia.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)

[**KSPROPERTY\_CAMERACONTROL\_S**](https://msdn.microsoft.com/library/windows/hardware/ff564439)

 

 






