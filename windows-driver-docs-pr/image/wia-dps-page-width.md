---
title: WIA \_ DPS \_ 页面 \_ 宽度
description: "\"WIA \\_ DPS \\_ 页面 \\_ 宽度\" 属性包含当前选定页面的宽度（以英寸的千分之几分之)  ( 001。"
keywords:
- WIA_DPS_PAGE_WIDTH 图像设备
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
ms.openlocfilehash: 7a478c32940a56328a78a560e31ac1d832414bc8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96831757"
---
# <a name="wia_dps_page_width"></a>WIA \_ DPS \_ 页面 \_ 宽度


"WIA \_ DPS \_ 页面 \_ 宽度" 属性包含当前选定页面的宽度（以英寸的千分之几分之)  ( 001。

## <span id="ddk_wia_dps_page_width_si"></span><span id="DDK_WIA_DPS_PAGE_WIDTH_SI"></span>


属性类型： VT \_ I4

有效值： WIA " \_ \_ 无"

访问权限：只读

<a name="remarks"></a>备注
-------

应用程序将读取 "WIA \_ DPS \_ 页面宽度" \_ 属性，以确定所扫描页面的物理尺寸。 如果范围设置不同于已知页面大小，则此属性将报告 " [**wia \_ DPS \_ 页面 \_ 大小**](wia-dps-page-size.md) " 属性设置为 "wia \_ 页面自定义" 的页面宽度 \_ 。 WIA 微型驱动程序创建并维护 WIA \_ DPS \_ 页面 \_ 宽度。

WIA \_ DPS \_ 页面 \_ 宽度必须提供等效于 [**WIA \_ IPS \_ XEXTENT**](wia-ips-xextent.md) 属性值的度量值，此值报告要扫描的页面的宽度（以像素为单位）。

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
<td><p>适用于 Microsoft Windows XP。 对于 Windows Vista 和更高版本，请使用相同的 WIA_IPS_PAGE_WIDTH 属性。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Wiadef (包含 Wiadef) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**WIA \_ DPS \_ 页面 \_ 高度**](wia-dps-page-height.md)

[**WIA \_ DPS \_ 页面 \_ 大小**](wia-dps-page-size.md)

[**WIA \_ IP \_ 页面 \_ 宽度**](wia-ips-page-width.md)

[**WIA \_ IP \_ XEXTENT**](wia-ips-xextent.md)

 

 






