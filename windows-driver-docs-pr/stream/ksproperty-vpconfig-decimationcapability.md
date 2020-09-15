---
title: KSPROPERTY \_ VPCONFIG \_ DECIMATIONCAPABILITY
description: KSPROPERTY \_ VPCONFIG \_ DECIMATIONCAPABILITY 属性指示是否可通过硬件降低视频图像的大小。
ms.assetid: a929b154-165e-4075-9295-d34fecc8e18d
keywords:
- KSPROPERTY_VPCONFIG_DECIMATIONCAPABILITY 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_VPCONFIG_DECIMATIONCAPABILITY
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5071cca97b57ba721887bb3ef38cfb65df0ebe1e
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90102690"
---
# <a name="ksproperty_vpconfig_decimationcapability"></a>KSPROPERTY \_ VPCONFIG \_ DECIMATIONCAPABILITY


KSPROPERTY \_ VPCONFIG \_ DECIMATIONCAPABILITY 属性指示是否可通过硬件降低视频图像的大小。

## <span id="ddk_ksproperty_vpconfig_decimationcapability_ks"></span><span id="DDK_KSPROPERTY_VPCONFIG_DECIMATIONCAPABILITY_KS"></span>


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
<td><p>否</p></td>
<td><p>Pin</p></td>
<td><p><a href="/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p>布尔</p></td>
</tr>
</tbody>
</table>

 

) 操作数据 (的属性值是一个布尔值。 如果硬件可以减少视频图像尺寸，则指定 **TRUE** ; 如果硬件无法减少尺寸，则指定 **FALSE** 。

<a name="remarks"></a>备注
-------

如果属性值为 **TRUE** ，则指定视频图像大小可减小。 **FALSE** 指定仍可调整图像大小，但也会将其剪裁到矩形而不是缩放。

KSPROPERTY \_ VPCONFIG \_ DECIMATION \_ 功能属性请求返回状态 " \_ 成功" 以指示成功完成。 否则，请求将返回相应的错误状态代码。

当 KSPROPSETID VPVBIConfig 使用此属性时 \_ ，所有属性请求都必须返回 \_ 未实现的状态 \_ 。

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
<td>Ksmedia (包含 Ksmedia) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**KSPROPERTY**](/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)

