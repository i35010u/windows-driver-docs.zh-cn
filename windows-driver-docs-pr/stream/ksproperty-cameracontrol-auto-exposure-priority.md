---
title: KSPROPERTY\_CAMERACONTROL\_自动\_暴露\_优先级
description: KSPROPERTY\_CAMERACONTROL\_自动\_暴露\_优先级属性指定是否在设备就可以动态更改帧速率。
ms.assetid: 0e20a4ee-b672-4c9a-9003-c2defd378e7c
keywords:
- KSPROPERTY_CAMERACONTROL_AUTO_EXPOSURE_PRIORITY 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_AUTO_EXPOSURE_PRIORITY
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: e4281db54d2058600cd2c96ade9d4a3edefab852
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63330299"
---
# <a name="kspropertycameracontrolautoexposurepriority"></a>KSPROPERTY\_CAMERACONTROL\_自动\_暴露\_优先级


KSPROPERTY\_CAMERACONTROL\_自动\_暴露\_优先级属性指定是否在设备就可以动态更改帧速率。

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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564439" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_S&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564439)"><strong>KSPROPERTY_CAMERACONTROL_S</strong></a>, <a href="https://msdn.microsoft.com/library/windows/hardware/ff564420" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_NODE_S&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564420)"><strong>KSPROPERTY_CAMERACONTROL_NODE_S</strong></a></p></td>
<td><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

属性值 （操作数据） 为指定帧速率是否可以动态变化的设备的 ULONG。

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
<td><p>帧速率必须保持不变。</p></td>
</tr>
<tr class="even">
<td><p>1</p></td>
<td><p>可以通过设备动态变化的帧速率。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

自动公开优先级确定摄像机是否可以动态更改根据光照条件的帧速率。

不自动公开，例如，如果帧速率为 30 fps 的暴露时间不能超过 33 毫秒。

自动公开优先级，但是，照相机可以补偿低光线通过降低帧速率。 例如，照相机可以减少为 25 fps，从而延长到 40 ms 的暴露时间的帧速率。

KSPROPERTY\_CAMERACONTROL\_自动\_暴露\_优先级将映射到**低亮度补偿**USB 视频类属性页上的复选框。

若要使用 KSPROPERTY\_CAMERACONTROL\_自动\_暴露\_优先级，必须设置[ **KSPROPERTY\_CAMERACONTROL\_暴露**](ksproperty-cameracontrol-exposure.md)为 auto。换而言之，照相机必须为自动公开模式为自动公开优先级模式作为有效的选项。

默认值为 KSPROPERTY\_CAMERACONTROL\_自动\_暴露\_优先级为零。

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


[**KSPROPERTY\_CAMERACONTROL\_S**](https://msdn.microsoft.com/library/windows/hardware/ff564439)

[**KSPROPERTY\_CAMERACONTROL\_节点\_S**](https://msdn.microsoft.com/library/windows/hardware/ff564420)

 

 






