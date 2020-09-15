---
title: KSPROPERTY \_ CAMERACONTROL \_ 自动 \_ 曝光 \_ 优先级
description: KSPROPERTY \_ CAMERACONTROL \_ 自动 \_ 曝光 \_ 优先级属性指定设备是否可以动态地改变帧速率。
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
ms.openlocfilehash: 5f6422b6f7cb31011991b4dce75338a382c7f2c7
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90107370"
---
# <a name="ksproperty_cameracontrol_auto_exposure_priority"></a>KSPROPERTY \_ CAMERACONTROL \_ 自动 \_ 曝光 \_ 优先级


KSPROPERTY \_ CAMERACONTROL \_ 自动 \_ 曝光 \_ 优先级属性指定设备是否可以动态地改变帧速率。

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
<td><p><a href="/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_S&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_s)"><strong>KSPROPERTY_CAMERACONTROL_S</strong></a>， <a href="/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_node_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_NODE_S&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_node_s)"> <strong>KSPROPERTY_CAMERACONTROL_NODE_S</strong></a></p></td>
<td><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

 (操作数据) 的属性值是一个 ULONG，用于指定帧速率是否可由设备动态变化。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>“值”</th>
<th>说明</th>
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

KSPROPERTY \_ CAMERACONTROL \_ 自动 \_ 曝光 \_ 优先级映射到 "USB 视频类" 属性页上的 " **低亮度补偿** " 复选框。

若要使用 KSPROPERTY \_ CAMERACONTROL \_ 自动 \_ 曝光 \_ 优先级，必须将 [**KSPROPERTY \_ CAMERACONTROL \_ 曝露**](ksproperty-cameracontrol-exposure.md) 设置为 auto。换句话说，照相机必须处于自动曝光模式下，自动曝光度优先级模式为有效选项。

KSPROPERTY \_ CAMERACONTROL \_ 自动曝光优先级的默认 \_ 值 \_ 为零。

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
<td>Ksmedia (包含 Ksmedia) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**KSPROPERTY \_ CAMERACONTROL \_ S**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_s)

[**KSPROPERTY \_ CAMERACONTROL \_ 节点 \_ S**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_node_s)

