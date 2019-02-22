---
title: WIA\_IPS\_颜色\_DROP\_绿色
description: WIA\_IPS\_颜色\_DROP\_绿色属性用于配置的绿色颜色通道 (G 中 RGB) 颜色下拉扩展量从 0 (无 dropout) 到 100 (完整通道 dropout) 范围内的一个百分比。
ms.assetid: 601BB830-034C-4A60-9F21-A1EBC45FDA8F
keywords:
- WIA_IPS_COLOR_DROP_GREEN 成像设备
topic_type:
- apiref
api_name:
- WIA_IPS_COLOR_DROP_GREEN
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 05/22/2018
ms.localizationpriority: medium
ms.openlocfilehash: ffb25ab4453e73d34e036c4a59d174d1d475773d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56548312"
---
# <a name="wiaipscolordropgreen"></a>WIA\_IPS\_颜色\_DROP\_绿色


**WIA\_IPS\_颜色\_DROP\_绿色**属性用于为介于 0%(no 百分比配置个绿色颜色通道 (G 中 RGB) 颜色下拉出量退出） 到 100%(完全通道 dropout)。 WIA 微型驱动程序创建并维护此属性。



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
<td><p>标头</p></td>
<td>Wiadef.h （包括 Wiadef.h）</td>
</tr>
</tbody>
</table>

 

 





