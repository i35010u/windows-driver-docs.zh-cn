---
title: KSPROPERTY\_CAMERACONTROL\_映像\_PIN\_功能\_属性
description: 用户模式下客户端使用此属性来确定是否照相机的图像插针和记录 pin 是互相排斥。 如果它们是互斥的然后记录 pin 处于活动状态时的图像插针不能为活动状态，并且进行相反转换。
ms.assetid: 4D000551-3AFB-4E14-9C67-EEDAB676AE03
keywords:
- KSPROPERTY_CAMERACONTROL_IMAGE_PIN_CAPABILITY_PROPERTY 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_IMAGE_PIN_CAPABILITY_PROPERTY
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4b322d031463b21c5f6452c74f4c188e4e07cb5d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63363167"
---
# <a name="kspropertycameracontrolimagepincapabilityproperty"></a>KSPROPERTY\_CAMERACONTROL\_映像\_PIN\_功能\_属性


用户模式下客户端使用此属性来确定是否照相机的图像插针和记录 pin 是互相排斥。 如果它们是互斥的然后记录 pin 处于活动状态时的图像插针不能为活动状态，并且进行相反转换。

## <span id="ddk_ksproperty_cameracontrol_pan_ks"></span><span id="DDK_KSPROPERTY_CAMERACONTROL_PAN_KS"></span>


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
<td><p>否</p></td>
<td><p>Filter</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><a href="https://msdn.microsoft.com/library/windows/hardware/jj553707" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_IMAGE_PIN_CAPABILITY_S&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/jj553707)"><strong>KSPROPERTY_CAMERACONTROL_IMAGE_PIN_CAPABILITY_S</strong></a></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

如果驱动程序实现此属性，并标识图像插针是独占使用记录 pin，媒体流式处理管道将防止进入该驱动程序进行录制时"take 照片"命令。

## <a name="see-also"></a>请参阅


[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)

[**KSPROPERTY\_CAMERACONTROL\_映像\_PIN\_功能\_S**](https://msdn.microsoft.com/library/windows/hardware/jj553707)

 

 






