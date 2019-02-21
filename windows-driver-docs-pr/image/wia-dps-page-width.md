---
title: WIA\_DPS\_页\_宽度
description: WIA\_DPS\_页\_宽度属性包含当前所选页上，在千分之几秒的英寸为单位的宽度 (。 001)。
ms.assetid: 02787660-3fb3-4e5d-ade8-b11ad29412c1
keywords:
- WIA_DPS_PAGE_WIDTH 成像设备
topic_type:
- apiref
api_name:
- WIA_DPS_PAGE_WIDTH
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 31e447b1a5f4f0d0926f64250762629840f72be9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544840"
---
# <a name="wiadpspagewidth"></a>WIA\_DPS\_页\_宽度


WIA\_DPS\_页\_宽度属性包含当前所选页上，在千分之几秒的英寸为单位的宽度 (。 001)。

## <span id="ddk_wia_dps_page_width_si"></span><span id="DDK_WIA_DPS_PAGE_WIDTH_SI"></span>


属性类型：VT\_I4

有效值：WIA\_PROP\_NONE

访问权限：只读

<a name="remarks"></a>备注
-------

应用程序读取 WIA\_DPS\_页\_WIDTH 属性来确定正在扫描的页的物理尺寸。 如果扩展盘区设置不同于已知的页面大小，此属性会将报告页的宽度其[ **WIA\_DPS\_页\_大小**](wia-dps-page-size.md)属性设置为WIA\_页\_自定义。 WIA 微型驱动程序创建和维护 WIA\_DPS\_页\_宽度。

WIA\_DPS\_页面\_宽度必须提供的值等效的度量[ **WIA\_IP\_大 XEXTENT** ](wia-ips-xextent.md)属性，宽度，以像素为单位，页后，可以扫描的报告。

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
<td><p>适用于 Microsoft Windows XP。 适用于 Windows Vista 及更高版本，使用相同的 WIA_IPS_PAGE_WIDTH 属性。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Wiadef.h （包括 Wiadef.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**WIA\_DPS\_PAGE\_HEIGHT**](wia-dps-page-height.md)

[**WIA\_DPS\_PAGE\_SIZE**](wia-dps-page-size.md)

[**WIA\_IPS\_PAGE\_WIDTH**](wia-ips-page-width.md)

[**WIA\_IPS\_XEXTENT**](wia-ips-xextent.md)

 

 






