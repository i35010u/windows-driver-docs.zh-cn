---
title: WIA\_DPS\_页\_高度
description: WIA\_DPS\_页\_高度属性包含的高度，以英寸为单位的千分之几秒 (。 001)，当前所选页面。 WIA 微型驱动程序创建并维护此属性。
ms.assetid: 93970d9a-96fe-4cf9-98c6-4ddcfd425214
keywords:
- WIA_DPS_PAGE_HEIGHT 成像设备
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
ms.openlocfilehash: 3a589ca1199be8449996903ab155a35f5f771cbb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56562475"
---
# <a name="wiadpspageheight"></a>WIA\_DPS\_页\_高度


WIA\_DPS\_页\_高度属性包含的高度，以英寸为单位的千分之几秒 (。 001)，当前所选页面。 WIA 微型驱动程序创建并维护此属性。

## <span id="ddk_wia_dps_page_height_si"></span><span id="DDK_WIA_DPS_PAGE_HEIGHT_SI"></span>


属性类型：VT\_I4

有效值：WIA\_PROP\_NONE

访问权限：只读

<a name="remarks"></a>备注
-------

应用程序读取 WIA\_DPS\_页\_高度，以确定正在扫描的页的物理尺寸。 如果扩展盘区设置不同于已知的页面大小，此属性会将报告页面的高度其[ **WIA\_DPS\_页\_大小**](wia-dps-page-size.md)属性设置为 WIA\_页上\_自定义 (它是一个值 WIA\_DPS\_页\_大小属性)。

WIA\_DPS\_页面\_高度必须提供英寸为单位，它等效于报告的像素值的千分之几秒的度量[ **WIA\_IP\_YEXTENT** ](wia-ips-yextent.md)属性，该报告的高度，以像素为单位，要进行扫描的页的属性。

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
<td><p>适用于 Microsoft Windows XP。 适用于 Windows Vista 及更高版本，使用相同的 WIA_IPS_PAGE_HEIGHT 属性。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Wiadef.h （包括 Wiadef.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**WIA\_DPS\_PAGE\_SIZE**](wia-dps-page-size.md)

[**WIA\_DPS\_PAGE\_WIDTH**](wia-dps-page-width.md)

[**WIA\_IPS\_PAGE\_HEIGHT**](wia-ips-page-height.md)

[**WIA\_IPS\_YEXTENT**](wia-ips-yextent.md)

 

 






