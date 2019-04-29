---
title: WIA\_IPS\_颜色\_DROP\_蓝色
description: WIA\_IPS\_颜色\_DROP\_蓝色属性用于配置的蓝色颜色通道 (B 中 RGB) 颜色下拉扩展量从 0 (无 dropout) 到 100 (完整通道 dropout) 范围内的一个百分比。
ms.assetid: AA3E633C-766A-4935-B942-6938D543F801
keywords:
- WIA_IPS_COLOR_DROP_BLUE 成像设备
topic_type:
- apiref
api_name:
- WIA_IPS_COLOR_DROP_BLUE
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 05/22/2018
ms.localizationpriority: medium
ms.openlocfilehash: fc39aeaf77c365f957cb1494a2c33b33dfc20d6b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63370805"
---
# <a name="wiaipscolordropblue"></a>WIA\_IPS\_颜色\_DROP\_蓝色


**WIA\_IPS\_颜色\_DROP\_蓝色**属性用于以百分比表示从 0%（否区域中配置的蓝色颜色通道 (B 中 RGB) 颜色下拉扩展量退出） 到 100%(完全通道 dropout)。 WIA 微型驱动程序创建并维护此属性。



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

 

 





