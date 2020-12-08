---
title: WIA \_ DPS \_ 页面 \_ 高度
description: "\"WIA \\_ DPS \\_ 页面 \\_ 高度\" 属性包含当前所选页面的高度（以英寸为单位） ( .001) 。 WIA 微型驱动程序创建并维护此属性。"
keywords:
- WIA_DPS_PAGE_HEIGHT 图像设备
topic_type:
- apiref
api_name:
- WIA_DPS_PAGE_HEIGHT
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: dfde55edae176d2b63ebb65592518b425ffb2c93
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96831761"
---
# <a name="wia_dps_page_height"></a>WIA \_ DPS \_ 页面 \_ 高度


"WIA \_ DPS \_ 页面 \_ 高度" 属性包含当前所选页面的高度（以英寸为单位） ( .001) 。 WIA 微型驱动程序创建并维护此属性。

## <span id="ddk_wia_dps_page_height_si"></span><span id="DDK_WIA_DPS_PAGE_HEIGHT_SI"></span>


属性类型： VT \_ I4

有效值： WIA " \_ \_ 无"

访问权限：只读

<a name="remarks"></a>备注
-------

应用程序将读取 WIA \_ DPS \_ 页 \_ 高度，以确定所扫描页面的物理尺寸。 如果范围设置不同于已知页面大小，则此属性将报告 "wia [**\_ dps \_ 页面 \_ 大小**](wia-dps-page-size.md) " 属性设置为 "wia 页面自定义 (" 的页面高度， \_ \_ 这是 "wia \_ dps \_ 页面大小" 属性的值 \_) 。

WIA \_ DPS \_ 页面 \_ 高度必须提供与 [**wia \_ IPS \_ YEXTENT**](wia-ips-yextent.md) 属性报告的像素值（以像素为单位）（报告要扫描的页面的高度（以像素为单位）相同的英寸的单位。

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
<td><p>适用于 Microsoft Windows XP。 对于 Windows Vista 和更高版本，请使用相同的 WIA_IPS_PAGE_HEIGHT 属性。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Wiadef (包含 Wiadef) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**WIA \_ DPS \_ 页面 \_ 大小**](wia-dps-page-size.md)

[**WIA \_ DPS \_ 页面 \_ 宽度**](wia-dps-page-width.md)

[**WIA \_ IP \_ 页面 \_ 高度**](wia-ips-page-height.md)

[**WIA \_ IP \_ YEXTENT**](wia-ips-yextent.md)

 

 






