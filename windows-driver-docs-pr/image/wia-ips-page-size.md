---
title: WIA \_ IP \_ 页面 \_ 大小
description: "\"WIA \\_ ip \\_ 页面 \\_ 大小\" 属性包含当前选定要扫描的页面的大小。"
ms.assetid: dcfad67e-31d5-41b8-b471-532626f571af
keywords:
- WIA_IPS_PAGE_SIZE 图像设备
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
ms.openlocfilehash: 1d1f17ff26c4845788e9e1d530a1d370371fc80a
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89185515"
---
# <a name="wia_ips_page_size"></a>WIA \_ IP \_ 页面 \_ 大小


"WIA \_ ip \_ 页面 \_ 大小" 属性包含当前选定要扫描的页面的大小。

属性类型： VT \_ I4

有效值： WIA 内容 \_ \_ 列表

访问权限：读/写

<a name="remarks"></a>注解
-------

若要选择要扫描的页的维度，应用程序将设置 "WIA \_ ip \_ 页面大小" \_ 属性。 WIA 微型驱动程序创建并维护此属性。

下表描述了对 WIA \_ ip 页面大小有效的常量 \_ \_ 。

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
<td><p>8267 x 11692 (纵向) 。</p></td>
</tr>
<tr class="even">
<td><p>WIA_PAGE_AUTO</p></td>
<td><p>用于配置自动页面大小检测。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_PAGE_CUSTOM</p></td>
<td><p>由 <a href="wia-ips-page-height.md" data-raw-source="[&lt;strong&gt;WIA_IPS_PAGE_HEIGHT&lt;/strong&gt;](wia-ips-page-height.md)"><strong>WIA_IPS_PAGE_HEIGHT</strong></a> 的值和 <a href="wia-ips-page-width.md" data-raw-source="[&lt;strong&gt;WIA_IPS_PAGE_WIDTH&lt;/strong&gt;](wia-ips-page-width.md)"><strong>WIA_IPS_PAGE_WIDTH</strong></a> 属性定义。</p></td>
</tr>
<tr class="even">
<td><p>WIA_PAGE_CUSTOM_BASE</p></td>
<td><p>由 WIA_IPS_PAGE_HEIGHT 的值和 WIA_IPS_PAGE_WIDTH 属性定义。 此值用于定义自定义页面大小，而不是 WIA_PAGE_CUSTOM 值启用的单个页面。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_PAGE_LETTER</p></td>
<td><p>8500 x 11000 (纵向) 。</p></td>
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
<td><p>在 Windows Vista 和更高版本的操作系统中可用。 对于 Windows XP，请改用 WIA_DPS_PAGE_SIZE 属性。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Wiadef (包含 Wiadef) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**IWiaMiniDrv：:d rvValidateItemProperties**](/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvvalidateitemproperties)

[**WIA \_ DPS \_ 页面 \_ 大小**](wia-dps-page-size.md)

[**WIA \_ IP \_ 方向**](wia-ips-orientation.md)

[**WIA \_ IP \_ 页面 \_ 高度**](wia-ips-page-height.md)

[**WIA \_ IP \_ 页面 \_ 宽度**](wia-ips-page-width.md)

[**WIA \_ IP \_ XEXTENT**](wia-ips-xextent.md)

[**WIA \_ IP \_ XPOS**](wia-ips-xpos.md)

[**WIA \_ IP \_ YEXTENT**](wia-ips-yextent.md)

[**WIA \_ IP \_ YPOS**](wia-ips-ypos.md)

 

