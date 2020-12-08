---
title: WIA \_ DPS \_ \_ 提前扫描 \_ 页面
description: WIA \_ DPS " \_ \_ 提前页" \_ 属性包含一个值，该值指示在将页面发送到应用程序之前，扫描程序是否会在扫描程序缓冲区中缓存页面。
keywords:
- WIA_DPS_SCAN_AHEAD_PAGES 图像设备
topic_type:
- apiref
api_name:
- WIA_DPS_SCAN_AHEAD_PAGES
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: b3791f54ea0c539bf0d834b59466344d56063094
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96831741"
---
# <a name="wia_dps_scan_ahead_pages"></a>WIA \_ DPS \_ \_ 提前扫描 \_ 页面


WIA \_ DPS " \_ \_ 提前页" \_ 属性包含一个值，该值指示在将页面发送到应用程序之前，扫描程序是否会在扫描程序缓冲区中缓存页面。

## <span id="ddk_wia_dps_scan_ahead_pages_si"></span><span id="DDK_WIA_DPS_SCAN_AHEAD_PAGES_SI"></span>


**注意**  此属性现已过时。 改为使用 [**WIA \_ ip \_ 扫描 \_**](wia-ips-scan-ahead.md) 。

 

属性类型： VT \_ I4

有效值： WIA \_ \_ (范围从零到文档送纸器可以容纳的最大页数) 

访问权限：读/写

<a name="remarks"></a>备注
-------

如果 WIA \_ DPS " \_ \_ 提前扫描 \_ 页" 属性为零，则将禁用 "提前扫描"，扫描程序将不会提前扫描任何页。

如果扫描程序在缓冲的预扫描项上执行数据传输，则扫描程序将检索缓冲页面。 在提前扫描操作期间，不能更改 WIA 属性。 WIA \_ DPS \_ \_ 提前扫描 \_ 页面是可选的。

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

## <a name="see-also"></a>请参阅


[**WIA \_ IP \_ \_ 提前扫描**](wia-ips-scan-ahead.md)

 

 






