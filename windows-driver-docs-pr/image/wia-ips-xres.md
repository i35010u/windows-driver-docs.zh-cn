---
title: WIA \_ IP \_ XRES
description: WIA \_ IPS \_ XRES 属性包含设备的当前水平分辨率（以每英寸像素为单位）。
keywords:
- WIA_IPS_XRES 图像设备
topic_type:
- apiref
api_name:
- WIA_IPS_XRES
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: d640d877b90a7df4293d1807fc3f101781f4e9b8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96816171"
---
# <a name="wia_ips_xres"></a>WIA \_ IP \_ XRES


WIA \_ IPS \_ XRES 属性包含设备的当前水平分辨率（以每英寸像素为单位）。

## <span id="ddk_wia_ips_xres_si"></span><span id="DDK_WIA_IPS_XRES_SI"></span>


属性类型： VT \_ I4

有效值： WIA "内容范围" 或 "WIA 内容" \_ \_ \_ \_ 列表

访问权限：读/写或只读

<a name="remarks"></a>备注
-------

应用程序设置 WIA \_ IPS \_ XRES 属性以设置水平分辨率。 WIA 微型驱动程序创建并维护此属性。

如果设备只能设置为单个值，请创建一个 WIA 的 " \_ \_ 类型"，并在其中放置有效值。 当一个分辨率设置依赖于另一种解决方法时，也会出现这种情况。  (例如，垂直分辨率可依赖于水平分辨率。 ) 

WIA \_ IPS \_ XRES 是所有支持映像采集的项目和存储的映像项目所必需的，它不适用于存储项目。

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


[**WIA \_ IP \_ XEXTENT**](wia-ips-xextent.md)

[**WIA \_ IP \_ XPOS**](wia-ips-xpos.md)

[**WIA \_ IP \_ YEXTENT**](wia-ips-yextent.md)

[**WIA \_ IP \_ YPOS**](wia-ips-ypos.md)

[**WIA \_ IP \_ YRES**](wia-ips-yres.md)

 

 






