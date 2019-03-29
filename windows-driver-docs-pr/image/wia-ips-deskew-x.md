---
title: WIA\_IPS\_反扭曲\_X
description: WIA\_IPS\_反扭曲\_X 属性，以及 WIA\_IP\_反扭曲\_Y 属性描述扭曲的图像的上两个角。 WIA 微型驱动程序创建并维护此属性。
ms.assetid: 0392d392-d814-4691-abb5-a8167bc101bb
keywords:
- WIA_IPS_DESKEW_X 成像设备
topic_type:
- apiref
api_name:
- WIA_IPS_DESKEW_X
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 147d4e6ad75831fb3d3b3ffb42b6b357adcc20b9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567631"
---
# <a name="wiaipsdeskewx"></a>WIA\_IPS\_反扭曲\_X


WIA\_IPS\_反扭曲\_X 属性，连同[ **WIA\_IP\_反扭曲\_Y** ](wia-ips-deskew-y.md)属性，介绍扭曲的图像上面的两个的角落。 WIA 微型驱动程序创建并维护此属性。

属性类型：VT\_I4

有效值：WIA\_PROP\_RANGE

访问权限：读取/写入

<a name="remarks"></a>备注
-------

WIA\_IPS\_反扭曲\_X 和 WIA\_IP\_反扭曲\_Y 属性描述的边框内扭曲的图像的两个右上角的位置该[ **WIA\_IP\_XPOS**](wia-ips-xpos.md)， [ **WIA\_IP\_YPOS**](wia-ips-ypos.md)， [**WIA\_IPS\_大 XEXTENT**](wia-ips-xextent.md)，并且[ **WIA\_IP\_YEXTENT** ](wia-ips-yextent.md)属性定义。

有效值为 WIA\_IPS\_反扭曲\_X 必须是介于 0 和 (WIA\_IP\_大 XEXTENT-1)。 值为 0 表示应执行任何偏斜的更正。

WIA\_IPS\_反扭曲\_X 不包含在从 WIA x 方向的像素数\_IP\_XPOS 到图像的最高的角的 x 坐标，以进行更正。

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
<td><p>在 Windows Vista 和更高版本操作系统中可用。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Wiadef.h （包括 Wiadef.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**WIA\_IPS\_反扭曲\_Y**](wia-ips-deskew-y.md)

[**WIA\_IPS\_XEXTENT**](wia-ips-xextent.md)

[**WIA\_IPS\_XPOS**](wia-ips-xpos.md)

[**WIA\_IPS\_YEXTENT**](wia-ips-yextent.md)

[**WIA\_IPS\_YPOS**](wia-ips-ypos.md)

 

 






