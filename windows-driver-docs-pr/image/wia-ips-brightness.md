---
title: WIA\_IP\_亮度
description: WIA\_IP\_亮度属性包含设备的当前硬件亮度设置。
ms.assetid: 3954cf52-3bb1-4b76-9ff4-a638e1ddde83
keywords:
- WIA_IPS_BRIGHTNESS 成像设备
topic_type:
- apiref
api_name:
- WIA_IPS_BRIGHTNESS
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: fcb6d628f90ced00b536eabb3ead2add23f47f20
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522247"
---
# <a name="wiaipsbrightness"></a>WIA\_IP\_亮度


WIA\_IP\_亮度属性包含设备的当前硬件亮度设置。

## <span id="ddk_wia_ips_brightness_si"></span><span id="DDK_WIA_IPS_BRIGHTNESS_SI"></span>


属性类型：VT\_I4

有效值：WIA\_PROP\_RANGE

访问权限：读取/写入

<a name="remarks"></a>备注
-------

应用程序设置 WIA\_IP\_亮度属性和硬件的亮度值。 WIA 微型驱动程序创建并维护此属性。

值为 WIA\_IP\_亮度应映射到 1000，其中 1000年对应于最大亮度、 0 对应于正常亮度和 −1000 对应于最小的亮度 −1000 从范围中。

WIA\_IP\_亮度是所必需的所有图像获取项。

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
<td>Wiadef.h （包括 Wiadef.h）</td>
</tr>
</tbody>
</table>

 

 





