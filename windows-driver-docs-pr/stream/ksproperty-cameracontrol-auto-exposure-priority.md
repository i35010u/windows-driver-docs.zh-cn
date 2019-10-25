---
title: KSPROPERTY\_CAMERACONTROL\_自动\_公开\_优先级
description: KSPROPERTY\_CAMERACONTROL\_自动\_公开\_PRIORITY 属性指定设备是否可以动态地改变帧速率。
ms.assetid: 0e20a4ee-b672-4c9a-9003-c2defd378e7c
keywords:
- KSPROPERTY_CAMERACONTROL_AUTO_EXPOSURE_PRIORITY 流媒体设备
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
ms.openlocfilehash: 3e40dc4c4f7b5affe9ca8af05d134d5573720614
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843252"
---
# <a name="ksproperty_cameracontrol_auto_exposure_priority"></a>KSPROPERTY\_CAMERACONTROL\_自动\_公开\_优先级


KSPROPERTY\_CAMERACONTROL\_自动\_公开\_PRIORITY 属性指定设备是否可以动态地改变帧速率。

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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_s)"><strong>KSPROPERTY_CAMERACONTROL_S</strong></a>、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_node_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_NODE_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_node_s)"> <strong>KSPROPERTY_CAMERACONTROL_NODE_S</strong></a></p></td>
<td><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

属性值（操作数据）是一个 ULONG，用于指定帧速率是否可由设备动态变化。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Value</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>0</p></td>
<td><p>帧速率必须保持不变。</p></td>
</tr>
<tr class="even">
<td><p>1</p></td>
<td><p>设备可以动态地改变帧速率。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

自动曝光优先级决定照相机是否可以根据光照条件动态变化帧速率。

如果没有自动曝光，例如，帧速率为 30 fps，则暴露时间不能超过33毫秒。

但对于自动曝光优先级，照相机可以通过降低帧速率来补偿低亮度。 例如，照相机可以将帧速率减少到 25 fps，从而将曝光时间延长至40毫秒。

KSPROPERTY\_CAMERACONTROL\_自动\_公开\_优先级映射到 "USB 视频类" 属性页上的 "**低亮度补偿**" 复选框。

若要使用 KSPROPERTY\_CAMERACONTROL\_自动\_公开\_优先级，必须将[**KSPROPERTY\_CAMERACONTROL\_公开**](ksproperty-cameracontrol-exposure.md)设置为 "自动"。换句话说，照相机必须处于自动曝光模式下，自动曝光度优先级模式为有效选项。

KSPROPERTY\_CAMERACONTROL\_自动\_\_公开的默认值为零。

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


[**KSPROPERTY\_CAMERACONTROL\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_s)

[**KSPROPERTY\_CAMERACONTROL\_NODE\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_node_s)

 

 






