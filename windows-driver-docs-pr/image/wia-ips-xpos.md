---
title: WIA \_ IP \_ XPOS
description: WIA \_ IPS \_ XPOS 属性包含所选图像的左上角的 x 坐标（以像素为单位）。 WIA 微型驱动程序创建并维护此属性。
keywords:
- WIA_IPS_XPOS 图像设备
topic_type:
- apiref
api_name:
- WIA_IPS_XPOS
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: fbaa87260c3b96623da4e162ddce19ad0141ef16
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96794935"
---
# <a name="wia_ips_xpos"></a>WIA \_ IP \_ XPOS


WIA \_ IPS \_ XPOS 属性包含所选图像的左上角的 x 坐标（以像素为单位）。 WIA 微型驱动程序创建并维护此属性。

## <span id="ddk_wia_ips_xpos_si"></span><span id="DDK_WIA_IPS_XPOS_SI"></span>


属性类型： VT \_ I4

有效值： WIA 内容 \_ \_ 范围

访问权限：读/写

<a name="remarks"></a>备注
-------

应用程序将 WIA \_ IPS \_ XPOS 属性设置为标记选择区域的左上角。

WIA \_ IPS \_ XPOS 对于所有启用了映像获取的项和这些项的子项是必需的; 此属性不可用于存储项或存储的图像项。

设置固定页面大小时，驱动程序必须设置 [**wia \_ ip \_ XEXTENT**](wia-ips-xextent.md)、Wia \_ ips \_ XPOS、 [**wia \_ ips \_ YEXTENT**](wia-ips-yextent.md)和 [**wia \_ ip \_ YPOS**](wia-ips-ypos.md) 属性，使其与页面大小大小和 "0" 原点匹配。 对于中心文档对齐，驱动程序必须将 WIA \_ ip \_ XPOS 设置为 ( # B1 扫描区域宽度-文档宽度) /2) \* 分辨率 \[ DPI \]) 和 WIA \_ ip \_ YPOS ( # B6 扫描区域高度-文档高度) /2) \* 分辨率 \[ DPI \]) 。

更改源或一个范围时，驱动程序必须将 [**wia \_ ip \_ 页面 \_ 大小**](wia-ips-page-size.md) 更新为 "自定义 \_ 大小"，并将 " [**Wia \_ ip \_ 页面 \_ 宽度**](wia-ips-page-width.md) " 和 " [**wia \_ ip 页面 \_ \_ 高度**](wia-ips-page-height.md) " 属性更新为与扫描区域范围匹配。 方向和旋转不应影响这些属性，除非方向改变 (不会改变旋转变化) 在可用文档扫描区域之外呈现原点或某个范围。

\_ \_ \_ \_ \_ \_ \_ \_ 当 [**wia \_ ip \_ XRES**](wia-ips-xres.md)和 [**WIA \_ ips \_ YRES**](wia-ips-yres.md)属性发生更改时，驱动程序还必须更新 wia ip XEXTENT、wia ips XPOS、wia ips YEXTENT 和 wia ip YPOS 属性。

**注意**   需要平板和胶卷子项才能仅支持 WIA \_ ip \_ XEXTENT、wia \_ IPS \_ XPOS、WIA \_ ips \_ XRES、wia \_ IP \_ YEXTENT、wia \_ ip \_ YPOS 和 wia \_ ip \_ YRES 属性。 对于其父级 ("基本" 或 "胶片" 项) 的所有其他属性（必需或可选）仅对这些项是可选的。 唯一的例外是 WIA \_ IPA \_ ITEM \_ *Xxx* 属性，所有项都需要这些属性。

 

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
<td>Wiadef (包含 Wiadef) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**WIA \_ IP \_ 页面 \_ 高度**](wia-ips-page-height.md)

[**WIA \_ IP \_ 页面 \_ 大小**](wia-ips-page-size.md)

[**WIA \_ IP \_ 页面 \_ 宽度**](wia-ips-page-width.md)

[**WIA \_ IP \_ XEXTENT**](wia-ips-xextent.md)

[**WIA \_ IP \_ XPOS**](wia-ips-xpos.md)

[**WIA \_ IP \_ XRES**](wia-ips-xres.md)

[**WIA \_ IP \_ YEXTENT**](wia-ips-yextent.md)

[**WIA \_ IP \_ YPOS**](wia-ips-ypos.md)

[**WIA \_ IP \_ YRES**](wia-ips-yres.md)

 

 






