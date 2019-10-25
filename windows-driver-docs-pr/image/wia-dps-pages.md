---
title: WIA\_DPS\_页
description: WIA\_DPS\_PAGES 属性包含要从自动文档送纸器中获取的当前页数。
ms.assetid: 51ab2eab-c7b4-4d54-bfc7-d53a8f66c7a9
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
ms.openlocfilehash: c456ebb34f89c3f12f4dd4a981e6ebfda733a4f6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840715"
---
# <a name="wia_dps_pages"></a>WIA\_DPS\_页


WIA\_DPS\_PAGES 属性包含要从自动文档送纸器中获取的当前页数。

## <span id="ddk_wia_dps_pages_si"></span><span id="DDK_WIA_DPS_PAGES_SI"></span>


属性类型： VT\_I4

有效值： WIA\_的\_范围（从零到扫描程序可扫描的最大页数）; 设置为零，\[0\] 持续扫描。）

访问权限：读/写

<a name="remarks"></a>备注
-------

应用程序将读取 WIA\_DPS\_PAGES 属性以确定文档送纸器的页容量。 应用程序还会将此属性设置为要扫描的页数。 WIA 微型驱动程序创建并维护 WIA\_DPS\_页面。

下表描述了对 WIA\_DPS\_PAGES 属性的有效常量。

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
<td><p>与将 WIA_PROP_RANGE 设置为零（0）相同。 所有页。 连续扫描，直到不能将更多文档送入 ADF。</p></td>
</tr>
</tbody>
</table>

 

**请注意**   如果启用了双工模式（即， [**WIA\_DPS\_文档\_处理\_选择**](wia-dps-document-handling-select.md)属性设置为 "进纸器 |双工），WIA\_DPS\_页面仍等于要扫描的页数。
如果启用了双工，则即使页面的背面为空白，一张纸也会自动包含两页。

如果将 WIA\_DPS\_页面设置为1，则扫描程序将处理页面的一方。 如果扫描程序在处于双工模式时无法只扫描页面的一侧，则应将[**wia\_属性\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/ns-wiamindr_lh-_wia_property_info)结构的**inc.** 的 "\_wia\_页" 值更改为 "2"。 此值向应用程序发出信号，指示该应用程序必须请求两个中的两个页面。 如果 WIA\_DPS\_页为零，则扫描程序将扫描当前加载到文档送纸器中的*所有*页面。

 

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
<td><p>适用于 Microsoft Windows XP。 对于 Windows Vista 和更高版本，请使用完全相同的 WIA_IPS_PAGES 属性。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Wiadef （包括 Wiadef）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**WIA\_DPS\_文档\_处理\_SELECT**](wia-dps-document-handling-select.md)

[**WIA\_IP\_页**](wia-ips-pages.md)

[**WIA\_属性\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/ns-wiamindr_lh-_wia_property_info)

 

 






