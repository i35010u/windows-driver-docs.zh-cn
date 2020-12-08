---
title: WIA \_ IP \_ \_ 提前扫描 \_ 容量
description: WIA \_ ip \_ 提前扫描 \_ 容量描述了扫描 \_ 程序可以提前扫描 (并将其存储在内部扫描器内存) 缓冲区中的最大页数， (当前文档大小、扫描分辨率、数据类型、文件格式、压缩等) 。 WIA 微型驱动程序创建并维护此属性。
keywords:
- WIA_IPS_SCAN_AHEAD_CAPACITY 图像设备
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
ms.openlocfilehash: a3df1496531a8572a003736686553bf81ee1335a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96783199"
---
# <a name="wia_ips_scan_ahead_capacity"></a>WIA \_ IP \_ \_ 提前扫描 \_ 容量


**WIA \_ ip \_ 提前扫描 \_ \_ 容量** 描述了扫描程序可以提前扫描 (并将其存储在内部扫描器内存) 缓冲区中的最大页数， (当前文档大小、扫描分辨率、数据类型、文件格式、压缩等) 。 WIA 微型驱动程序创建并维护此属性。




属性类型： VT \_ UI4

有效值： WIA " \_ \_ 无"

访问权限：读/写

<a name="remarks"></a>备注
-------

支持 " [**wia \_ ip \_ 扫描 \_ 提前**](wia-ips-scan-ahead.md) " 属性时，此属性仅对 " (WIA 类别送纸器) 的进纸器项有效 \_ \_ ，并且是可选的。

值0表示 "未定义/未知的页数"。

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

 

 





