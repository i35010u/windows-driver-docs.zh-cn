---
title: WIA\_IP\_页
description: WIA\_IPS\_PAGES "属性包含要从自动文档送纸器中获取的当前页数。
ms.assetid: 638f816b-0efd-4885-b285-4fa6a42272bc
keywords:
- WIA_IPS_PAGES 图像设备
topic_type:
- apiref
api_name:
- WIA_IPS_PAGES
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 72d237bb3fed1abcb74e01c97f0daf91fdd01c73
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840685"
---
# <a name="wia_ips_pages"></a>WIA\_IP\_页


WIA\_IPS\_PAGES "属性包含要从自动文档送纸器中获取的当前页数。

属性类型： VT\_I4

有效值： WIA\_的值\_范围（零到扫描程序可扫描的最大页数）; 设置为零（0）表示连续扫描）

访问权限：读/写

<a name="remarks"></a>备注
-------

应用程序会读取 WIA\_IPS\_页，以确定文档送纸器的页容量。 应用程序将此属性设置为在当前 WIA 会话中要扫描的最大页数。 WIA 微型驱动程序创建并维护此属性。

下表描述了对 WIA\_IPS\_页有效的常量。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Value</th>
<th>定义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>ALL_PAGES</p></td>
<td><p>连续扫描，直到不能将更多文档送入 ADF。 此值与将 WIA_PROP_RANGE 设置为零（0）相同。</p></td>
</tr>
</tbody>
</table>

 

**请注意**   如果启用了双工模式（即，如果 WIA\_IPS\_文档\_处理\_SELECT 已设置为 "进纸器 |双工），WIA\_IPS\_页面仍等于要扫描的页数。
如果启用了双工，则即使页面的背面为空白，一张纸也会自动包含两页。

如果将 WIA\_IPS\_页面设置为1，则扫描程序将处理页面的一方。 如果扫描程序在处于双工模式时无法只扫描页面的一侧，则应将[**wia\_属性\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/ns-wiamindr_lh-_wia_property_info)结构的**INC.** 成员的 WIA\_IPS\_页面值更改为2。 对于此值，应用程序必须请求两个中的两个页面。 如果值为零，则表示扫描当前加载到文档送纸器中的*所有*页面。

 

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
<td><p>在 Windows Vista 和更高版本的操作系统中可用。 对于 Windows XP，请改为使用 WIA_DPS_PAGES 属性。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Wiadef （包括 Wiadef）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**WIA\_DPS\_页**](wia-dps-pages.md)

[**WIA\_属性\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/ns-wiamindr_lh-_wia_property_info)

 

 






