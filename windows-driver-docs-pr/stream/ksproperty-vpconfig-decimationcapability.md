---
title: KSPROPERTY\_VPCONFIG\_DECIMATIONCAPABILITY
description: KSPROPERTY\_VPCONFIG\_DECIMATIONCAPABILITY 属性指示是否视频图像的大小可以减少硬件。
ms.assetid: a929b154-165e-4075-9295-d34fecc8e18d
keywords:
- KSPROPERTY_VPCONFIG_DECIMATIONCAPABILITY 流式处理媒体设备
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
ms.openlocfilehash: 6a5844e0d8918bc423fdad8fc248759d76fecc86
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522859"
---
# <a name="kspropertyvpconfigdecimationcapability"></a>KSPROPERTY\_VPCONFIG\_DECIMATIONCAPABILITY


KSPROPERTY\_VPCONFIG\_DECIMATIONCAPABILITY 属性指示是否视频图像的大小可以减少硬件。

## <span id="ddk_ksproperty_vpconfig_decimationcapability_ks"></span><span id="DDK_KSPROPERTY_VPCONFIG_DECIMATIONCAPABILITY_KS"></span>


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
<td><p>Pin</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p>布尔</p></td>
</tr>
</tbody>
</table>

 

属性值 （操作数据） 是一个布尔值。 指定 **，则返回 TRUE**如果硬件可以减小视频图像尺寸，或者指定**FALSE**如果硬件不能减少维度。

<a name="remarks"></a>备注
-------

属性值 **，则返回 TRUE**指定视频图像可缩小大小。 **FALSE**指定映像仍可进行调整，但还会向该矩形剪裁而不是扩展。

KSPROPERTY\_VPCONFIG\_抽取\_功能属性请求返回状态\_成功以指示成功完成。 否则，请求将返回相应的错误状态代码。

此属性由 KSPROPSETID\_VPVBIConfig，属性的所有请求必须都返回状态\_不\_实现。

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

 

 






