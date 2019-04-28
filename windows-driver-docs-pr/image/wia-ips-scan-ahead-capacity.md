---
title: WIA\_IPS\_扫描\_预先\_容量
description: WIA\_IPS\_扫描\_预先\_容量描述当前扫描作业设置 （当前在最大数目的页扫描程序可继续扫描 （并在内部扫描程序内存缓冲区中存储）文档大小、 扫描解析、 数据类型、 文件格式、 压缩和等等）。 WIA 微型驱动程序创建并维护此属性。
ms.assetid: 7A80964D-B0A4-4D6B-A320-4DE0A700E1A9
keywords:
- WIA_IPS_SCAN_AHEAD_CAPACITY 成像设备
topic_type:
- apiref
api_name:
- WIA_IPS_SCAN_AHEAD_CAPACITY
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 05/22/2018
ms.localizationpriority: medium
ms.openlocfilehash: 5b217831f3282502a17c0376a7ced3fa18f6e9ea
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63343885"
---
# <a name="wiaipsscanaheadcapacity"></a>WIA\_IPS\_扫描\_预先\_容量


**WIA\_IPS\_扫描\_预先\_容量**描述当前在扫描程序可以继续扫描 （在内部扫描程序内存缓冲区中存储） 的最大页数扫描作业设置 （当前文档大小、 扫描分辨率、 数据类型、 文件格式、 压缩和等等）。 WIA 微型驱动程序创建并维护此属性。




属性类型：VT\_UI4

有效值：WIA\_PROP\_NONE

访问权限：读/写

<a name="remarks"></a>备注
-------

当[ **WIA\_IPS\_扫描\_预先**](wia-ips-scan-ahead.md)支持属性，此属性仅对送纸器项有效 (WIA\_类别\_送纸器)，并且是可选的。

值为 0 表示"未定义/未知的页的数目"。

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

 

 





