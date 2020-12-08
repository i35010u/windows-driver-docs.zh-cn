---
title: WIA \_ DPS \_ 页面
description: WIA \_ DPS \_ PAGES 属性包含要从自动文档送纸器中获取的当前页数。
keywords:
- WIA_DPS_PAGES 图像设备
topic_type:
- apiref
api_name:
- WIA_DPS_PAGES
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: f4a286bf13cfdd734bfa16fa677f93a437463c58
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96831751"
---
# <a name="wia_dps_pages"></a>WIA \_ DPS \_ 页面


WIA \_ DPS \_ PAGES 属性包含要从自动文档送纸器中获取的当前页数。

## <span id="ddk_wia_dps_pages_si"></span><span id="DDK_WIA_DPS_PAGES_SI"></span>


属性类型： VT \_ I4

有效值： WIA \_ \_ (范围从零到扫描程序可扫描的页数上限; 设置为零0则表示 \[ \] 持续扫描。 ) 

访问权限：读/写

<a name="remarks"></a>备注
-------

应用程序读取 "WIA \_ DPS \_ 页面" 属性以确定文档送纸器的页面容量。 应用程序还会将此属性设置为要扫描的页数。 WIA 微型驱动程序创建并维护 WIA \_ DPS \_ 页面。

下表描述了对 WIA \_ DPS PAGES 属性有效的常量 \_ 。

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
<td><p>ALL_PAGES</p></td>
<td><p>与将 WIA_PROP_RANGE 设置为零 (0) 相同。 所有页。 连续扫描，直到不能将更多文档送入 ADF。</p></td>
</tr>
</tbody>
</table>

 

**注意**   如果启用了双工模式 (即， [**WIA \_ DPS \_ 文档 \_ 处理 \_ 选择**](wia-dps-document-handling-select.md) 属性将设置为 "馈送器 |双工) ，WIA \_ DPS \_ 页面仍等于要扫描的页数。
如果启用了双工，则即使页面的背面为空白，一张纸也会自动包含两页。

如果将 "WIA \_ DPS \_ 页面" 设置为 "1"，则扫描程序将处理页面的一方。 如果扫描程序在处于双工模式时无法只扫描页面的一侧，则应将 \_ \_ [**wia \_ 属性 \_ 信息**](/windows-hardware/drivers/ddi/wiamindr_lh/ns-wiamindr_lh-_wia_property_info)结构的 **inc.** 的 "wia DPS 页面" 值更改为 "2"。 此值向应用程序发出信号，指示该应用程序必须请求两个中的两个页面。 如果 WIA \_ DPS \_ 页面为零，扫描程序将扫描当前加载到文档送纸器中的 *所有* 页面。

 

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
<td><p>适用于 Microsoft Windows XP。 对于 Windows Vista 和更高版本，请使用相同的 WIA_IPS_PAGES 属性。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Wiadef (包含 Wiadef) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**WIA \_ DPS \_ 文档 \_ 处理 \_ 选择**](wia-dps-document-handling-select.md)

[**WIA \_ IP \_ 页面**](wia-ips-pages.md)

[**WIA \_ 属性 \_ 信息**](/windows-hardware/drivers/ddi/wiamindr_lh/ns-wiamindr_lh-_wia_property_info)

 

