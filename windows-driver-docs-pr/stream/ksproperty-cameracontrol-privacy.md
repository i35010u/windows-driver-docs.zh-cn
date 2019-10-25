---
title: KSPROPERTY\_CAMERACONTROL\_隐私
description: KSPROPERTY\_CAMERACONTROL\_隐私属性指定是否阻止相机传感器获取视频。
ms.assetid: 6a96301e-b4f1-4d4d-9cc6-f0cb1e2c1391
keywords:
- KSPROPERTY_CAMERACONTROL_PRIVACY 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_PRIVACY
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4671e996d90d21586e28cecb3d3e764c4ce9f54e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842491"
---
# <a name="ksproperty_cameracontrol_privacy"></a>KSPROPERTY\_CAMERACONTROL\_隐私


KSPROPERTY\_CAMERACONTROL\_隐私属性指定是否阻止相机传感器获取视频。

## <span id="ddk_ksproperty_cameracontrol_privacy_ks"></span><span id="DDK_KSPROPERTY_CAMERACONTROL_PRIVACY_KS"></span>


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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_s)"><strong>KSPROPERTY_CAMERACONTROL_S</strong></a>或<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_node_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_NODE_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_node_s)"> <strong>KSPROPERTY_CAMERACONTROL_NODE_S</strong></a></p></td>
<td><p>漫长</p></td>
</tr>
</tbody>
</table>

 

属性值（操作数据）是指定是否启用或禁用隐私模式的 LONG。 如果值为0，则表示相机传感器可以捕获视频图像，值为1表示阻止相机传感器捕获视频图像。

<a name="remarks"></a>备注
-------

KSPROPERTY\_CAMERACONTROL\_NODE\_结构的**值**成员指定相机传感器是否应捕获视频。

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


[**KSPROPERTY\_CAMERACONTROL\_NODE\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_node_s)

 

 






