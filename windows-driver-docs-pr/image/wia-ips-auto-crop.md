---
title: WIA\_IPS\_AUTO\_CROP
description: WIA\_IPS\_自动\_裁剪属性用于启用自动检测和裁剪来扫描区域的设备。 WIA 微型驱动程序创建并维护此属性。
ms.assetid: 5D7D2911-1535-4E67-9EBF-2B59D87F4F1B
keywords:
- WIA_IPS_AUTO_CROP 成像设备
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
ms.openlocfilehash: 7612e7ddc6065b74b7ea6581ea25eabd50f3b331
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63381503"
---
# <a name="wiaipsautocrop"></a>WIA\_IPS\_AUTO\_CROP


**WIA\_IPS\_自动\_裁剪**属性用于启用自动检测和裁剪来扫描区域的设备。 WIA 微型驱动程序创建并维护此属性。




属性类型：VT\_I4

有效值：WIA\_PROP\_列表

访问权限：读/写

<a name="remarks"></a>备注
-------

下表描述了的有效值**WIA\_IPS\_自动\_裁剪**属性。

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
<td><p>WIA_AUTO_CROP_DISABLED</p></td>
<td><p>禁用自动裁剪。 如果支持该属性，这是所需的默认值。</p></td>
</tr>
<tr class="even">
<td><p>WIA_AUTO_CROP_SINGLE</p></td>
<td><p>启用自动裁剪。 一个扫描区域将检测并裁剪每个文档页面上。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_AUTO_CROP_MULTI</p></td>
<td><p>启用自动裁剪。 检测和裁剪每个文档页面上的一个或多个扫描区域。 作为一个单页面文件或多页文件中的新页面，每个裁剪后的扫描区域传输到 WIA 应用程序客户端。</p></td>
</tr>
</tbody>
</table>

 

此属性是有效的和可选的送纸器 (WIA\_类别\_送纸器) 项，它可以带或不带 WIA 实现\_页面\_自动值[ **WIA\_IPS\_页上\_大小**](wia-ips-page-size.md)属性。 此属性也是有效 （和可选） 对于平板 (WIA\_类别\_平板) 和电影胶片 (WIA\_类别\_电影) 的项，但如果 WIAWIA微型驱动程序不支持分段\_类别\_平板和 WIA\_类别\_电影输入源。 如果 WIA\_IPS\_支持划分网段然后 WIA\_IPS\_自动\_裁剪无效，不能在同一时间支持。

支持的属性，当 WIA\_自动\_裁剪\_DISABLED 和至少一个其他两个可能值 (WIA\_自动\_裁剪\_单和/或 WIA\_自动\_裁剪\_多) 是必需的使用 WIA\_自动\_裁剪\_禁用所需的默认值。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Wiadef.h （包括 Wiadef.h）</td>
</tr>
</tbody>
</table>

 

 





