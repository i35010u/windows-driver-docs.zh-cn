---
title: WIA\_IPS\_颜色\_DROP\_红色
description: WIA\_IPS\_颜色\_DROP\_红色属性用于配置的红色颜色通道 (R 中 RGB) 颜色下拉扩展量从 0 (无 dropout) 到 100 (完整通道 dropout) 范围内的一个百分比。
ms.assetid: B241154C-0F4F-4800-A8CD-30831F1AB25B
keywords:
- WIA_IPS_COLOR_DROP_RED 成像设备
topic_type:
- apiref
api_name:
- WIA_IPS_COLOR_DROP_RED
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 05/22/2018
ms.localizationpriority: medium
ms.openlocfilehash: e4085ce5c989428efc2bba45728ef495e463b89c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63325041"
---
# <a name="wiaipscolordropred"></a>WIA\_IPS\_颜色\_DROP\_红色


**WIA\_IPS\_颜色\_DROP\_RED**属性用于配置的红色颜色通道 (R 中 RGB) 颜色下拉扩展的大小，范围从 0%(没有 dropout) 中的一个百分比为 100%(完全通道 dropout)。 WIA 微型驱动程序创建并维护此属性。



属性类型：VT\_I4 | VT\_VECTOR

有效值：WIA\_PROP\_NONE

访问权限：读/写

<a name="remarks"></a>备注
-------

当[ **WIA\_IPS\_颜色\_DROP** ](wia-ips-color-drop.md)支持属性，此属性是有效的所有可编程图像数据源项，包括平板 (WIA\_类别\_平板) 和送纸器 (WIA\_类别\_送纸器)，并且需要。 此属性的有效值为 0 到 100 (含) 之间。

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

 

 





