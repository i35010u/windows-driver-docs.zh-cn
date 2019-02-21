---
title: WIA\_IPS\_反扭曲\_Y
description: WIA\_IPS\_反扭曲\_Y 属性，以及 WIA\_IP\_反扭曲\_X 属性，描述扭曲的图像的上两个角。 WIA 微型驱动程序创建并维护此属性。
ms.assetid: 25aca00f-4048-4784-90a1-f1ad8c2de16a
keywords:
- WIA_IPS_DESKEW_Y 成像设备
topic_type:
- apiref
api_name:
- WIA_IPS_DESKEW_Y
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 927e4957661e93d3bdceb6227cd6a9498c2e39a2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56545051"
---
# <a name="wiaipsdeskewy"></a>WIA\_IPS\_反扭曲\_Y


WIA\_IPS\_反扭曲\_Y 属性一起[ **WIA\_IP\_反扭曲\_X** ](wia-ips-deskew-x.md)属性，介绍扭曲的图像上面的两个的角落。 WIA 微型驱动程序创建并维护此属性。

属性类型：VT\_I4

有效值：WIA\_PROP\_RANGE

访问权限：读取/写入

<a name="remarks"></a>备注
-------

WIA\_IPS\_反扭曲\_X 和 WIA\_IP\_反扭曲\_Y 属性描述的边框内扭曲的图像的两个右上角的位置的[**WIA\_IPS\_XPOS**](wia-ips-xpos.md)， [ **WIA\_IP\_YPOS**](wia-ips-ypos.md)， [ **WIA\_IP\_大 XEXTENT**](wia-ips-xextent.md)，和[ **WIA\_IP\_YEXTENT** ](wia-ips-yextent.md)属性定义。

有效值为 WIA\_IPS\_反扭曲\_Y 必须介于 0 和 (WIA\_IP\_YEXTENT-1)。 值为 0 表示应执行任何反扭曲。

WIA\_IPS\_反扭曲\_Y 包含从 WIA y 方向的像素数\_IP\_YPOS 到图像的最左侧的角的 y 坐标，以将 deskewed。

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
<td><p>标头</p></td>
<td>Wiadef.h （包括 Wiadef.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**WIA\_IPS\_DESKEW\_X**](wia-ips-deskew-x.md)

[**WIA\_IPS\_XEXTENT**](wia-ips-xextent.md)

[**WIA\_IPS\_XPOS**](wia-ips-xpos.md)

[**WIA\_IPS\_YEXTENT**](wia-ips-yextent.md)

[**WIA\_IPS\_YPOS**](wia-ips-ypos.md)

 

 






