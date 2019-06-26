---
title: WIA\_IPS\_PAGES
description: WIA\_IP\_页属性包含要获取自动文档送纸器中的页的数目。
ms.assetid: 638f816b-0efd-4885-b285-4fa6a42272bc
keywords:
- WIA_IPS_PAGES 成像设备
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
ms.openlocfilehash: d47cd0a6b495a0971f73117dfd6ac200736bc0b9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385303"
---
# <a name="wiaipspages"></a>WIA\_IPS\_PAGES


WIA\_IP\_页属性包含要获取自动文档送纸器中的页的数目。

属性类型：VT\_I4

有效值：WIA\_PROP\_范围 (0 到扫描仪可以扫描; 设置为零 (0)，以持续扫描最大页数)

访问权限：读取/写入

<a name="remarks"></a>备注
-------

应用程序读取 WIA\_IP\_页面，以确定文档送纸器的页上的容量。 应用程序设置此属性是愿意扫描当前 WIA 会话中的页面的最大数目。 WIA 微型驱动程序创建并维护此属性。

下表描述了常量，它是有效使用 WIA\_IP\_页。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>ReplTest1</th>
<th>定义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>ALL_PAGES</p></td>
<td><p>没有更多文档送入 ADF 之前一直扫描。 此值等同于将 WIA_PROP_RANGE 设置为零 (0)。</p></td>
</tr>
</tbody>
</table>

 

**请注意**  如果启用了双工模式 (即，如果 WIA\_IP\_文档\_处理\_选择设置为送纸器 |双工），WIA\_IP\_页是否仍等于要扫描的页数。
一张纸将自动包含两个页面如果启用双工，则即使该页的后端为空。

如果设置 WIA\_IP\_页为 1，扫描程序将处理页面的方面之一。 我们建议，如果无法扫描的页中双工模式仅一侧扫描程序，您应更改 WIA\_IPS\_页值**Inc**的成员[ **WIA\_属性\_INFO** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/ns-wiamindr_lh-_wia_property_info)为 2 的结构。 利用此值，该应用程序必须请求中的两个序列图的页面。 值为零意味着*所有*当前加载到文档送纸器的页面都要进行扫描。

 

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Version</p></td>
<td><p>在 Windows Vista 和更高版本操作系统中可用。 对于 Windows XP 中，而是使用 WIA_DPS_PAGES 属性。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Wiadef.h （包括 Wiadef.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**WIA\_DPS\_PAGES**](wia-dps-pages.md)

[**WIA\_属性\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/ns-wiamindr_lh-_wia_property_info)

 

 






