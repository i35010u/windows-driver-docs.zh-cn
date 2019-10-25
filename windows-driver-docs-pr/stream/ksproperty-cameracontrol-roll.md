---
title: KSPROPERTY\_CAMERACONTROL\_滚动
description: 用户模式客户端使用 KSPROPERTY\_CAMERACONTROL\_滚动属性来获取或设置照相机的滚动设置。 此属性为可选项。
ms.assetid: 58b09e8d-7c0c-4e32-b124-5722bd09f011
keywords:
- KSPROPERTY_CAMERACONTROL_ROLL 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_ROLL
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ea4343a3df475a1884b42e40293ba5a6d4a0ab62
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72826913"
---
# <a name="ksproperty_cameracontrol_roll"></a>KSPROPERTY\_CAMERACONTROL\_滚动


用户模式客户端使用 KSPROPERTY\_CAMERACONTROL\_滚动属性来获取或设置照相机的滚动设置。 此属性为可选项。

## <span id="ddk_ksproperty_cameracontrol_roll_ks"></span><span id="DDK_KSPROPERTY_CAMERACONTROL_ROLL_KS"></span>


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

 

属性值（操作数据）是指定相机滚动设置的 LONG。 此值以度为单位表示。

正值会使相机沿图像查看轴顺时针旋转。 负值将导致照相机逆时针旋转，如下图所示。

![显示照相机滚动值的图示](images/cam-roll-1.png)

支持此属性的每个视频捕获微型驱动程序都必须为此属性定义一个范围和默认值。 设备的范围必须为-180 到 + 180，并且默认值必须为0。

<a name="remarks"></a>备注
-------

KSPROPERTY\_CAMERACONTROL\_S 结构的**值**成员指定了滚动设置。

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
<td>Ksmedia （包括 Ksmedia）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)

[**KSPROPERTY\_CAMERACONTROL\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_s)

 

 






