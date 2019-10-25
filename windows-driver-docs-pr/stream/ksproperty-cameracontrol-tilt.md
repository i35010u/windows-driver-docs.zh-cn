---
title: KSPROPERTY\_CAMERACONTROL\_倾斜
description: 用户模式客户端使用 KSPROPERTY\_CAMERACONTROL\_倾斜属性来获取或设置相机的倾斜设置。 此属性为可选项。
ms.assetid: 265315ce-6f35-4f5a-907f-b5595e7fb5af
keywords:
- KSPROPERTY_CAMERACONTROL_TILT 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_TILT
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: a4e66166604023b658300d4c4f4b0d72b09a0c41
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842487"
---
# <a name="ksproperty_cameracontrol_tilt"></a>KSPROPERTY\_CAMERACONTROL\_倾斜


用户模式客户端使用 KSPROPERTY\_CAMERACONTROL\_倾斜属性来获取或设置相机的倾斜设置。 此属性为可选项。

## <span id="ddk_ksproperty_cameracontrol_tilt_ks"></span><span id="DDK_KSPROPERTY_CAMERACONTROL_TILT_KS"></span>


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

 

属性值（操作数据）是指定相机倾斜设置的 LONG。 此值以度为单位表示。

正值表示图像平面上滑面。 负值表示成像面朝下，如下图所示。

![显示相机斜度值的图示](images/cam-tilt-1.png)

支持此属性的每个视频捕获微型驱动程序都必须为此属性定义一个范围和默认值。 设备的范围必须为-180 到 + 180。 默认值必须为0。

**警告**  编写或测试应用程序时，应注意，在实际情况下，某些驱动程序会定义倾斜值的自定义范围以及可能不基于典型单位的自定义步长值。 驱动程序可能会以物理方式或数字方式实现倾斜控件。

 

<a name="remarks"></a>备注
-------

KSPROPERTY\_CAMERACONTROL\_S 结构的**值**成员指定倾斜设置。

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

 

 






