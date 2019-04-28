---
title: WIA\_IP\_YRES
description: WIA\_IP\_YRES 属性包含当前垂直分辨率设置，以每英寸点数，设备的像素为单位。
ms.assetid: 40a98cac-e5de-42db-b9df-1fba63925427
keywords:
- WIA_IPS_YRES 成像设备
topic_type:
- apiref
api_name:
- WIA_IPS_YRES
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 964256c44e62ae2f4ee206c9f7323a76ab8ceb3f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327845"
---
# <a name="wiaipsyres"></a>WIA\_IP\_YRES


WIA\_IP\_YRES 属性包含当前垂直分辨率设置，以每英寸点数，设备的像素为单位。

## <span id="ddk_wia_ips_yres_si"></span><span id="DDK_WIA_IPS_YRES_SI"></span>


属性类型：VT\_I4

有效值：WIA\_PROP\_范围或 WIA\_PROP\_列表

访问权限：读/写或只读的

<a name="remarks"></a>备注
-------

应用程序设置 WIA\_IP\_YRES 属性设置的垂直分辨率。 WIA 微型驱动程序创建并维护此属性。

如果设备可以设置为单个值，创建 WIA\_PROP\_列表类型并将有效的值放入其中。 一种解决方法设置依赖于另一个解决方法时，这种情况下也适用。 （例如，垂直分辨率可以依赖于的水平分辨率。）

WIA\_IP\_YRES 是所有图像采集启用项目和存储的图像项所必需的; 它不是可用于存储项。

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


[**WIA\_IPS\_XEXTENT**](wia-ips-xextent.md)

[**WIA\_IPS\_XPOS**](wia-ips-xpos.md)

[**WIA\_IPS\_XRES**](wia-ips-xres.md)

[**WIA\_IPS\_YEXTENT**](wia-ips-yextent.md)

[**WIA\_IPS\_YPOS**](wia-ips-ypos.md)

 

 






