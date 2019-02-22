---
title: WIA\_IPS\_XRES
description: WIA\_IP\_XRES 属性包含以像素为单位的每英寸点数，设备的当前水平分辨率。
ms.assetid: cde64e80-b4b0-4360-a14e-b6918b97aabc
keywords:
- WIA_IPS_XRES 成像设备
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
ms.openlocfilehash: 776c63f2cb7d6be7c520f67fae64f0a0770e2c92
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554619"
---
# <a name="wiaipsxres"></a>WIA\_IPS\_XRES


WIA\_IP\_XRES 属性包含以像素为单位的每英寸点数，设备的当前水平分辨率。

## <span id="ddk_wia_ips_xres_si"></span><span id="DDK_WIA_IPS_XRES_SI"></span>


属性类型：VT\_I4

有效值：WIA\_PROP\_范围或 WIA\_PROP\_列表

访问权限：读/写或只读的

<a name="remarks"></a>备注
-------

应用程序设置 WIA\_IP\_XRES 属性设置的水平分辨率。 WIA 微型驱动程序创建并维护此属性。

如果设备可以设置为单个值，创建 WIA\_PROP\_列表类型并将有效的值放入其中。 一种解决方法设置依赖于另一个解决方法时，这种情况下也适用。 （例如，垂直分辨率可以依赖于的水平分辨率。）

WIA\_IP\_XRES 是所有图像采集启用项目和存储的图像项所必需的; 它不是可用于存储项。

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

## <a name="see-also"></a>另请参阅


[**WIA\_IPS\_XEXTENT**](wia-ips-xextent.md)

[**WIA\_IPS\_XPOS**](wia-ips-xpos.md)

[**WIA\_IPS\_YEXTENT**](wia-ips-yextent.md)

[**WIA\_IPS\_YPOS**](wia-ips-ypos.md)

[**WIA\_IPS\_YRES**](wia-ips-yres.md)

 

 






