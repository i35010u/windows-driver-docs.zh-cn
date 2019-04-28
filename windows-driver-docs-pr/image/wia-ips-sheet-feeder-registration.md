---
title: WIA\_IPS\_表\_送纸器\_注册
description: WIA\_IPS\_表\_送纸器\_注册属性包含的注册，或对齐方式和边缘检测，放置在扫描程序的平台的文档。 WIA 微型驱动程序创建并维护此属性。
ms.assetid: d97d5784-3360-48a3-a24e-97b4238c42f5
keywords:
- WIA_IPS_SHEET_FEEDER_REGISTRATION 成像设备
topic_type:
- apiref
api_name:
- WIA_IPS_SHEET_FEEDER_REGISTRATION
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: bc2516bbc397836a660921f9bc2689d224bf679d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63343859"
---
# <a name="wiaipssheetfeederregistration"></a>WIA\_IPS\_表\_送纸器\_注册


WIA\_IPS\_表\_送纸器\_注册属性包含的注册，或对齐方式和边缘检测，放置在扫描程序的平台的文档。 WIA 微型驱动程序创建并维护此属性。

属性类型：VT\_I4

有效值：WIA\_PROP\_NONE

访问权限：只读

<a name="remarks"></a>备注
-------

WIA\_IPS\_表\_送纸器\_注册属性指示文档如何水平定位在手持设备或工作表提供扫描程序扫描头上。 可以使用 WIA\_IPS\_表\_送纸器\_注册来预测在扫描头文档放置的位置。

下表描述了有效使用 WIA 的常量\_IPS\_表\_送纸器\_注册。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Constant</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>LEFT_JUSTIFIED</p></td>
<td><p>该文档位于相对于扫描头左侧。</p></td>
</tr>
<tr class="even">
<td><p>居中</p></td>
<td><p>扫描标头是以文档为中心。</p></td>
</tr>
<tr class="odd">
<td><p>RIGHT_JUSTIFIED</p></td>
<td><p>该文档位于相对于扫描头右侧。</p></td>
</tr>
</tbody>
</table>

 

为支持多个扫描仪扫描 head WIA\_IPS\_表\_送纸器\_注册属性相对于的最顶层扫描头。 此属性是必需的纸、 滚动馈送和手持扫描仪。

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
<td><p>在 Windows Vista 和更高版本操作系统中可用。 对于 Windows XP 中，而是使用 WIA_DPS_SHEET_FEEDER_REGISTRATION 属性。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Wiadef.h （包括 Wiadef.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**WIA\_DPS\_表\_送纸器\_注册**](wia-dps-sheet-feeder-registration.md)

 

 






