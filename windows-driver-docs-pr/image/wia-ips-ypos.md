---
title: WIA\_IPS\_YPOS
description: WIA\_IP\_YPOS 属性包含的当前 y 坐标，以像素为单位的所选图像的左上角。 WIA 微型驱动程序创建并维护此属性。
ms.assetid: e6592d54-d1b6-4ee7-8678-903d575d52a3
keywords:
- WIA_IPS_YPOS 成像设备
topic_type:
- apiref
api_name:
- WIA_IPS_YPOS
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 54d6867205c28896c78285a7d9eccf727dafd858
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63363050"
---
# <a name="wiaipsypos"></a>WIA\_IPS\_YPOS


WIA\_IP\_YPOS 属性包含的当前 y 坐标，以像素为单位的所选图像的左上角。 WIA 微型驱动程序创建并维护此属性。

## <span id="ddk_wia_ips_ypos_si"></span><span id="DDK_WIA_IPS_YPOS_SI"></span>


属性类型：VT\_I4

有效值：WIA\_PROP\_RANGE

访问权限：读取/写入

<a name="remarks"></a>备注
-------

应用程序设置 WIA\_IP\_YPOS 属性来标记所选内容区域的左上角。

WIA\_IP\_YPOS 是必需的所有图像启用获取的项和子项的这些项; 此属性不是可用于存储项目或存储的图像项。

当固定的页面大小设置时，驱动程序必须设置[ **WIA\_IPS\_大 XEXTENT**](wia-ips-xextent.md)， [ **WIA\_IP\_XPOS** ](wia-ips-xpos.md)， [ **WIA\_IP\_YEXTENT**](wia-ips-yextent.md)，并**WIA\_IP\_YPOS**属性以匹配页面大小维度和"0"的起始位置。 对于 center 文档对齐方式，该驱动程序必须设置 WIA\_IPS\_XPOS 到 (（扫描区域宽度的文档的宽度） / 2)\*解析\[DPI\]) 和 WIA\_IP\_YPOS 为 （（扫描区高度的文档高度） / 2)\*解析\[DPI\])。

该驱动程序的源或一个扩展盘区更改时，必须更新[ **WIA\_IPS\_页\_大小**](wia-ips-page-size.md)属性设置为自定义\_大小和[**WIA\_IPS\_页面\_宽度**](wia-ips-page-width.md)并[ **WIA\_IP\_页\_高度** ](wia-ips-page-height.md)属性以匹配的扫描区域扩展盘区。 方向和旋转应不会影响这些属性，除非方向更改 （不是一个旋转更改） 将呈现的源或可用的文档扫描区之外的一个扩展盘区。

驱动程序还必须更新 WIA\_IPS\_大 XEXTENT、 WIA\_IPS\_XPOS、 WIA\_IP\_YEXTENT 和 WIA\_IP\_YPOS 属性时[ **WIA\_IP\_XRES** ](wia-ips-xres.md)并[ **WIA\_IP\_YRES** ](wia-ips-yres.md)更改属性。

**请注意**  平板和电影胶片子项目所需支持仅 WIA\_IPS\_大 XEXTENT、 WIA\_IP\_XPOS、 WIA\_IP\_XRES，WIA\_IPS\_YEXTENT、 WIA\_IPS\_YPOS 和 WIA\_IP\_YRES 属性。 所有其他属性，必需或可选的其父 （基平板或电影项），只是可选的这些项。 唯一的例外是 WIA\_IPA\_项\_*Xxx*属性，所需的所有项。

 

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
<td>Wiadef.h （包括 Wiadef.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**WIA\_IPS\_PAGE\_HEIGHT**](wia-ips-page-height.md)

[**WIA\_IPS\_PAGE\_SIZE**](wia-ips-page-size.md)

[**WIA\_IPS\_PAGE\_WIDTH**](wia-ips-page-width.md)

[**WIA\_IPS\_XEXTENT**](wia-ips-xextent.md)

[**WIA\_IPS\_XPOS**](wia-ips-xpos.md)

[**WIA\_IPS\_XRES**](wia-ips-xres.md)

[**WIA\_IPS\_YEXTENT**](wia-ips-yextent.md)

[**WIA\_IPS\_YRES**](wia-ips-yres.md)

 

 






