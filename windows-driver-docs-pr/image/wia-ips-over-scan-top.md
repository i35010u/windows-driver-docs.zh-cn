---
title: WIA \_ IP \_ OVER \_ 扫描 \_ 顶部
description: 使用 WIA \_ ip \_ over \_ scan \_ TOP 属性和 wia ips over scan，将使用 wia ip over SCAN， \_ \_ \_ \_ \_ \_ \_ \_ 并使用 wia \_ ips \_ over \_ scan \_ 来配置与物理文档相关的扫描量（以英寸 (0.001 \ 0034; ) 单位为单位）。
keywords:
- WIA_IPS_OVER_SCAN_TOP 图像设备
topic_type:
- apiref
api_name:
- WIA_IPS_OVER_SCAN_TOP
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 05/22/2018
ms.localizationpriority: medium
ms.openlocfilehash: 02ac4dd00d4f06f4aa0ab7e28be7018b275ad272
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96823133"
---
# <a name="wia_ips_over_scan_top"></a>WIA \_ IP \_ OVER \_ 扫描 \_ 顶部


使用 **wia \_ ip \_ over \_ Scan \_ TOP** 属性和 [**wia \_ ips \_ over \_ \_**](wia-ips-over-scan-bottom.md)scan，将使用 [**wia \_ \_ \_ \_**](wia-ips-over-scan-left.md)ip over scan，并使用 [**wia \_ ips \_ over \_ scan \_**](wia-ips-over-scan-right.md) 来配置相对于物理文档的扫描量（以英寸为单位 (0.001 ") 单位）。 WIA 微型驱动程序创建并维护此属性。




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

 

 





