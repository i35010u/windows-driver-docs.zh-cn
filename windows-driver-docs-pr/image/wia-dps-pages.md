---
title: WIA\_DPS\_PAGES
description: WIA\_DPS\_页属性包含要获取自动文档送纸器中的页的数目。
ms.assetid: 51ab2eab-c7b4-4d54-bfc7-d53a8f66c7a9
keywords:
- WIA_DPS_PAGES 成像设备
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
ms.openlocfilehash: 5f0289268f58ceffcb92c04873d35546fbd3cb4f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543188"
---
# <a name="wiadpspages"></a>WIA\_DPS\_PAGES


WIA\_DPS\_页属性包含要获取自动文档送纸器中的页的数目。

## <span id="ddk_wia_dps_pages_si"></span><span id="DDK_WIA_DPS_PAGES_SI"></span>


属性类型：VT\_I4

有效值：WIA\_PROP\_范围 (从 0 到扫描仪可以扫描; 设置为零的最大页数\[0\]连续扫描。)

访问权限：读取/写入

<a name="remarks"></a>备注
-------

应用程序读取 WIA\_DPS\_页属性来确定文档送纸器页容量。 应用程序还将此属性设置为它要扫描的页数。 WIA 微型驱动程序创建和维护 WIA\_DPS\_页。

下表描述了常量，它是有效使用 WIA\_DPS\_页属性。

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
<td><p>与将 WIA_PROP_RANGE 设置为零 (0) 相同。 所有页面。 没有更多文档送入 ADF 之前一直扫描。</p></td>
</tr>
</tbody>
</table>

 

**请注意**  如果启用了双工模式 (即[ **WIA\_DPS\_文档\_处理\_选择**](wia-dps-document-handling-select.md)属性设置为送纸器 |双工），WIA\_DPS\_页是否仍等于要扫描的页数。
一张纸将自动包含两个页面如果启用双工，则即使该页的后端为空。

如果设置 WIA\_DPS\_页为 1，扫描程序将处理页面的方面之一。 如果扫描程序不能扫描的页中双工模式仅一侧，则应更改 WIA\_DPS\_页值**Inc**的成员[ **WIA\_属性\_INFO** ](https://msdn.microsoft.com/library/windows/hardware/ff552751)为 2 的结构。 此值向发出信号，该应用程序，它必须请求中的两个序列图的页面。 如果 WIA\_DPS\_页为零，则扫描程序将扫描*所有*当前加载到文档送纸器的页。

 

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
<td><p>适用于 Microsoft Windows XP。 适用于 Windows Vista 及更高版本，使用相同的 WIA_IPS_PAGES 属性。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Wiadef.h （包括 Wiadef.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**WIA\_DPS\_文档\_处理\_选择**](wia-dps-document-handling-select.md)

[**WIA\_IPS\_PAGES**](wia-ips-pages.md)

[**WIA\_属性\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff552751)

 

 






