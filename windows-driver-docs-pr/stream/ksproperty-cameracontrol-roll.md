---
title: KSPROPERTY\_CAMERACONTROL\_回滚
description: 用户模式下客户端使用 KSPROPERTY\_CAMERACONTROL\_汇总属性来获取或设置照相机的前设置。 此属性为可选项。
ms.assetid: 58b09e8d-7c0c-4e32-b124-5722bd09f011
keywords:
- KSPROPERTY_CAMERACONTROL_ROLL 流式处理媒体设备
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
ms.openlocfilehash: d4b8da38c16b73f78ba016cc962a93e71ac64152
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373181"
---
# <a name="kspropertycameracontrolroll"></a>KSPROPERTY\_CAMERACONTROL\_回滚


用户模式下客户端使用 KSPROPERTY\_CAMERACONTROL\_汇总属性来获取或设置照相机的前设置。 此属性为可选项。

## <span id="ddk_ksproperty_cameracontrol_roll_ks"></span><span id="DDK_KSPROPERTY_CAMERACONTROL_ROLL_KS"></span>


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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_cameracontrol_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_cameracontrol_s)"><strong>KSPROPERTY_CAMERACONTROL_S</strong> </a>或<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_cameracontrol_node_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_NODE_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_cameracontrol_node_s)"> <strong>KSPROPERTY_CAMERACONTROL_NODE_S</strong></a></p></td>
<td><p>长</p></td>
</tr>
</tbody>
</table>

 

属性值 （操作数据） 为指定照相机的前设置长时间。 此值表示以度为单位。

正值会导致该图像查看轴照相机的顺时针旋转。 负值会导致开始沿逆时针方向旋转照相机，如以下插图所示。

![图显示相机汇总值](images/cam-roll-1.png)

每个视频捕获微型驱动程序支持此属性必须定义此属性的范围和默认值。 设备的范围必须是介于-180 到 180 和默认值必须为 0。

<a name="remarks"></a>备注
-------

**值**KSPROPERTY 成员\_CAMERACONTROL\_S 结构指定前设置。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Ksmedia.h （包括 Ksmedia.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)

[**KSPROPERTY\_CAMERACONTROL\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_cameracontrol_s)

 

 






