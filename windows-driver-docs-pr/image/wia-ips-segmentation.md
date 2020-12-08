---
title: WIA \_ IPS \_ 分段
description: WIA \_ IPS \_ 分段属性指示在扫描过程中是否要执行分段。 WIA 微型驱动程序创建并维护此属性。
keywords:
- WIA_IPS_SEGMENTATION 图像设备
topic_type:
- apiref
api_name:
- WIA_IPS_SEGMENTATION
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: e8487e82c2508bba230b6cc5547ac6611af2f267
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96808723"
---
# <a name="wia_ips_segmentation"></a>WIA \_ IPS \_ 分段


WIA \_ IPS \_ 分段属性指示在扫描过程中是否要执行分段。 WIA 微型驱动程序创建并维护此属性。

属性类型： VT \_ I4

有效值： WIA " \_ \_ 无"

访问权限：只读

<a name="remarks"></a>备注
-------

下表描述了为 "WIA IPS 分段" 属性定义的值 \_ \_ 。

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
<td><p>WIA_USE_SEGMENTATION_FILTER</p></td>
<td><p>应用程序应使用分段筛选器进行多区域扫描。</p></td>
</tr>
<tr class="even">
<td><p>WIA_DONT_USE_SEGMENTATION_FILTER</p></td>
<td><p>驱动程序为多区域扫描创建子项目本身。 如果扫描程序使用固定帧进行多区域扫描，通常会发生这种情况。</p></td>
</tr>
</tbody>
</table>

 

\_ \_ 如果扫描仪平板和胶卷项支持使用分段筛选器创建子项，或者驱动程序本身为固定框架创建子项，则必须实现 WIA ip 分段。

您可以使用分段筛选器打包驱动程序，并且仍将 WIA \_ ip \_ 分段设置为 wia 请勿 \_ \_ 使用 \_ 分段 \_ 筛选器项 (例如，胶片项) 。 如果扫描程序使用固定帧进行胶片扫描，而不是从平板扫描，则会发生这种情况。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>标头</p></td>
<td>Wiadef (包含 Wiadef) </td>
</tr>
</tbody>
</table>

 

 





