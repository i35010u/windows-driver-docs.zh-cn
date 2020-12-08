---
title: WIA \_ IPS \_ 自动 \_ 裁剪
description: WIA \_ IPS \_ 自动 \_ 裁剪属性用于启用扫描区域的设备的自动检测和裁剪。 WIA 微型驱动程序创建并维护此属性。
keywords:
- WIA_IPS_AUTO_CROP 图像设备
topic_type:
- apiref
api_name:
- WIA_IPS_AUTO_CROP
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1c8d8c62e23c3ed6197be22b24afc17095e9d23d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96824461"
---
# <a name="wia_ips_auto_crop"></a>WIA \_ IPS \_ 自动 \_ 裁剪


**WIA \_ IPS \_ 自动 \_ 裁剪** 属性用于启用扫描区域的设备的自动检测和裁剪。 WIA 微型驱动程序创建并维护此属性。




属性类型： VT \_ I4

有效值： WIA 内容 \_ \_ 列表

访问权限：读/写

<a name="remarks"></a>备注
-------

下表描述了 " **WIA \_ IPS \_ 自动 \_ 裁剪** " 属性的有效值。

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
<td><p>WIA_AUTO_CROP_DISABLED</p></td>
<td><p>自动裁剪处于禁用状态。 如果支持该属性，则这是所需的默认值。</p></td>
</tr>
<tr class="even">
<td><p>WIA_AUTO_CROP_SINGLE</p></td>
<td><p>启用自动裁剪。 每个文档页上检测并裁剪一个扫描区域。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_AUTO_CROP_MULTI</p></td>
<td><p>启用自动裁剪。 在每个文档页上检测并裁剪一个或多个扫描区域。 每个裁剪扫描区域都作为单个页面文件或作为多页面文件中的新页传输到 WIA 应用程序客户端。</p></td>
</tr>
</tbody>
</table>

 

此属性对于送纸器 (WIA \_ 类别 \_ 进纸器) 项是有效的，并且可用于在 " \_ \_ [**wia \_ ip \_ 页面 \_ 大小**](wia-ips-page-size.md) " 属性中不带 wia 页面自动值的情况下实现它。 此属性还有效 (和可选) ，适用于平板 (WIA \_ 类别的 \_ 平板) 和胶片 (wia \_ 类别 \_ 胶片) 项，但仅当 wia 的 wia 小型驱动程序 \_ \_ 和 wia \_ 类别 \_ 胶片输入源不支持分段。 如果 \_ 支持 wia ips SEGEMENTATION，则 \_ wia \_ ips \_ 自动 \_ 裁剪无效，不能同时支持。

如果支持该属性，则 \_ 禁用 wia 自动 \_ 裁剪， \_ 并且至少需要另外两个值中的一个 (wia \_ 自动 \_ 裁剪 \_ 单一和/或 wia \_ 自动 \_ 裁剪 \_ 多) ，而禁用了 wia 自动裁剪 \_ \_ \_ 。

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

 

 





