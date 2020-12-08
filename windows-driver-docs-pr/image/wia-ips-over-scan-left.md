---
title: WIA \_ IPS \_ OVER \_ SCAN \_
description: "\"WIA \\_ ip \\_ over \\_ scan\" \\_ 属性连同 \"wia \\_ ip \\_ over \\_ 扫描 \\_ \" 权限一起使用，通过 \"扫描\" 顶部的 \\_ \"wia ip\" \\_ \\_ 和 \"wia ips over 扫描\"， \\_ \\_ \\_ \\_ \\_ 可用于配置与物理文档相关的扫描量（以英寸 (0.001 \\ 0034; ) 单位为单位）。"
keywords:
- WIA_IPS_OVER_SCAN_LEFT 图像设备
topic_type:
- apiref
api_name:
- WIA_IPS_OVER_SCAN_LEFT
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 05/22/2018
ms.localizationpriority: medium
ms.openlocfilehash: dbc45b148422322032257cc25da0e33c5ce762cb
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96823137"
---
# <a name="wia_ips_over_scan_left"></a>WIA \_ IPS \_ OVER \_ SCAN \_


使用 " **wia ip \_ \_ over \_ Scan \_** " 属性连同 [**wia \_ ip \_ 在 "扫描" \_ \_ 权限**](wia-ips-over-scan-right.md)上，使用 "wia Ip over 扫描"，并使用 "使用 [**\_ \_ \_ 扫描 \_ 底部的 wia ip**](wia-ips-over-scan-bottom.md) " 来配置与物理文档相关的扫描量（以英寸为单位 (0.001 ") 单位）。 [**\_ \_ \_ \_**](wia-ips-over-scan-top.md) WIA 微型驱动程序创建并维护此属性。




属性类型： VT \_ UI4

有效值： WIA 内容 \_ \_ 范围

访问权限：读/写

<a name="remarks"></a>备注
-------

此属性对所有可编程的图像数据源项有效，包括平板 (WIA \_ 类别 \_ 平板) 和送纸器 (wia \_ 类别 \_ 进纸器) 但仅当支持 [**wia \_ ip \_ OVER \_ SCAN**](wia-ips-over-scan.md) 属性时。 如果支持该属性，则此属性是必需的。

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

 

 





