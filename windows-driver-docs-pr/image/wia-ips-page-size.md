---
title: WIA\_IPS\_PAGE\_SIZE
description: WIA\_IPS\_页\_SIZE 属性包含当前选定要扫描的页的大小。
ms.assetid: dcfad67e-31d5-41b8-b471-532626f571af
keywords:
- WIA_IPS_PAGE_SIZE 成像设备
topic_type:
- apiref
api_name:
- WIA_IPS_PAGE_SIZE
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 95cf34fd77cf26fab0e9c56158b14ff36a1ab240
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555491"
---
# <a name="wiaipspagesize"></a>WIA\_IPS\_PAGE\_SIZE


WIA\_IPS\_页\_SIZE 属性包含当前选定要扫描的页的大小。

属性类型：VT\_I4

有效值：WIA\_PROP\_列表

访问权限：读取/写入

<a name="remarks"></a>备注
-------

若要选择要扫描的页的尺寸，应用程序在设置 WIA\_IPS\_页\_大小属性。 WIA 微型驱动程序创建并维护此属性。

下表描述了有效使用 WIA 的常量\_IPS\_页\_大小。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>值</th>
<th>定义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>WIA_PAGE_A4</p></td>
<td><p>8267 × 11692 （纵向）。</p></td>
</tr>
<tr class="even">
<td><p>WIA_PAGE_AUTO</p></td>
<td><p>用于配置自动页大小检测。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_PAGE_CUSTOM</p></td>
<td><p>值定义的<a href="wia-ips-page-height.md" data-raw-source="[&lt;strong&gt;WIA_IPS_PAGE_HEIGHT&lt;/strong&gt;](wia-ips-page-height.md)"> <strong>WIA_IPS_PAGE_HEIGHT</strong> </a>并<a href="wia-ips-page-width.md" data-raw-source="[&lt;strong&gt;WIA_IPS_PAGE_WIDTH&lt;/strong&gt;](wia-ips-page-width.md)"> <strong>WIA_IPS_PAGE_WIDTH</strong> </a>属性。</p></td>
</tr>
<tr class="even">
<td><p>WIA_PAGE_CUSTOM_BASE</p></td>
<td><p>定义由 WIA_IPS_PAGE_HEIGHT 和 WIA_IPS_PAGE_WIDTH 属性的值。 此值用于定义自定义页面大小，而不是 WIA_PAGE_CUSTOM 值允许单个页。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_PAGE_LETTER</p></td>
<td><p>8500 × 11000 （纵向）。</p></td>
</tr>
</tbody>
</table>

 

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
<td><p>在 Windows Vista 和更高版本操作系统中可用。 对于 Windows XP 中，而是使用 WIA_DPS_PAGE_SIZE 属性。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Wiadef.h （包括 Wiadef.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**IWiaMiniDrv::drvValidateItemProperties**](https://msdn.microsoft.com/library/windows/hardware/ff545017)

[**WIA\_DPS\_PAGE\_SIZE**](wia-dps-page-size.md)

[**WIA\_IP\_方向**](wia-ips-orientation.md)

[**WIA\_IPS\_PAGE\_HEIGHT**](wia-ips-page-height.md)

[**WIA\_IPS\_PAGE\_WIDTH**](wia-ips-page-width.md)

[**WIA\_IPS\_XEXTENT**](wia-ips-xextent.md)

[**WIA\_IPS\_XPOS**](wia-ips-xpos.md)

[**WIA\_IPS\_YEXTENT**](wia-ips-yextent.md)

[**WIA\_IPS\_YPOS**](wia-ips-ypos.md)

 

 






