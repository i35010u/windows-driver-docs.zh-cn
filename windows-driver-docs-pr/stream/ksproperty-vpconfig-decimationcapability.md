---
title: KSPROPERTY\_VPCONFIG\_DECIMATIONCAPABILITY
description: KSPROPERTY\_VPCONFIG\_DECIMATIONCAPABILITY 属性指示是否可通过硬件降低视频图像的大小。
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
ms.openlocfilehash: ae25af8099b552ceb95f7aa614b05b2da07af537
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842815"
---
# <a name="ksproperty_vpconfig_decimationcapability"></a>KSPROPERTY\_VPCONFIG\_DECIMATIONCAPABILITY


KSPROPERTY\_VPCONFIG\_DECIMATIONCAPABILITY 属性指示是否可通过硬件降低视频图像的大小。

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
<td><p>无</p></td>
<td><p>大头针</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p>布尔型</p></td>
</tr>
</tbody>
</table>

 

属性值（操作数据）为布尔值。 如果硬件可以减少视频图像尺寸，则指定**TRUE** ; 如果硬件无法减少尺寸，则指定**FALSE** 。

<a name="remarks"></a>备注
-------

如果属性值为**TRUE** ，则指定视频图像大小可减小。 **FALSE**指定仍可调整图像大小，但也会将其剪裁到矩形而不是缩放。

KSPROPERTY\_VPCONFIG\_DECIMATION\_功能属性请求返回状态\_SUCCESS，指示成功完成。 否则，请求将返回相应的错误状态代码。

当 KSPROPSETID\_VPVBIConfig 使用此属性时，所有属性请求都必须返回状态，\_不\_实现。

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

 

 






