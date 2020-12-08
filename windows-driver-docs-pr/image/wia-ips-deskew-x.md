---
title: WIA \_ IP \_ 反扭曲 \_ X
description: WIA \_ ip \_ 抗扭反 \_ X 属性与 wia \_ ip \_ 反扭曲 \_ Y 属性一起介绍了倾斜图像的上两个角。 WIA 微型驱动程序创建并维护此属性。
keywords:
- WIA_IPS_DESKEW_X 图像设备
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
ms.openlocfilehash: 8e1802c8e38f2b6fd8d7e133af3c4c77c7f84bad
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96796139"
---
# <a name="wia_ips_deskew_x"></a>WIA \_ IP \_ 反扭曲 \_ X


WIA \_ ip \_ 抗扭反 \_ X 属性与 [**wia \_ ip \_ 反扭曲 \_ Y**](wia-ips-deskew-y.md) 属性一起介绍了倾斜图像的上两个角。 WIA 微型驱动程序创建并维护此属性。

属性类型： VT \_ I4

有效值： WIA 内容 \_ \_ 范围

访问权限：读/写

<a name="remarks"></a>备注
-------

WIA ip \_ \_ 反扭曲 \_ X 和 WIA \_ ip \_ 反扭曲 \_ Y 属性说明了在 [**WIA \_ ip \_ XPOS**](wia-ips-xpos.md)、 [**wia \_ ip \_ YPOS**](wia-ips-ypos.md)、 [**wia \_ ips \_ XEXTENT**](wia-ips-xextent.md)和 [**wia \_ ip \_ YEXTENT**](wia-ips-yextent.md) 属性定义的边框内，扭曲图像的两个顶角所在的位置。

WIA \_ ip \_ 反扭曲 X 的有效值 \_ 必须介于0和 (WIA \_ ip \_ XEXTENT-1) 之间。 值0表示不应执行任何歪斜更正。

WIA \_ ip \_ 抗扭斜 \_ x 包含 x 方向从 WIA \_ ips \_ XPOS 到要更正的图像最上方的 x 坐标的像素数。

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
<td><p>在 Windows Vista 和更高版本的操作系统中可用。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Wiadef (包含 Wiadef) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**WIA \_ IP \_ 抗扭反 \_ Y**](wia-ips-deskew-y.md)

[**WIA \_ IP \_ XEXTENT**](wia-ips-xextent.md)

[**WIA \_ IP \_ XPOS**](wia-ips-xpos.md)

[**WIA \_ IP \_ YEXTENT**](wia-ips-yextent.md)

[**WIA \_ IP \_ YPOS**](wia-ips-ypos.md)

 

 






