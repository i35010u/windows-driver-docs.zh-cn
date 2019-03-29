---
title: WIA\_IPS\_转移\_扫描\_左侧
description: WIA\_IP\_转移\_扫描\_左边缘的属性以及 WIA\_IP\_通过\_扫描\_右、 WIA\_IP\_转移\_扫描\_上边缘和 WIA\_IPS\_转移\_扫描\_底部用于通过扫描英寸为单位的千分之几秒中配置的金额 (0.001 \ 0034;)单元，相对于物理文档。
ms.assetid: D1C2ADF5-A38C-4E30-A377-E62C5B4208A6
keywords:
- WIA_IPS_OVER_SCAN_LEFT 成像设备
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
ms.openlocfilehash: 8e1868a67a629f2e519e1de2fb12a4fecefce085
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566284"
---
# <a name="wiaipsoverscanleft"></a>WIA\_IPS\_转移\_扫描\_左侧


**WIA\_IPS\_转移\_扫描\_左侧**属性连同[ **WIA\_IP\_通过\_扫描\_右**](wia-ips-over-scan-right.md)， [ **WIA\_IP\_通过\_扫描\_顶部**](wia-ips-over-scan-top.md)，和[ **WIA\_IP\_转移\_扫描\_底部**](wia-ips-over-scan-bottom.md)用于通过扫描千分之一英寸 （0.001 英寸） 单元中配置的量相对于物理文档。 WIA 微型驱动程序创建并维护此属性。




属性类型：VT\_UI4

有效值：WIA\_PROP\_RANGE

访问权限：读/写

<a name="remarks"></a>备注
-------

此属性仅适用于所有可编程图像数据源项，包括平板 (WIA\_类别\_平板) 和送纸器 (WIA\_类别\_送纸器)，但仅当[ **WIA\_IPS\_转移\_扫描**](wia-ips-over-scan.md)支持属性。 如果支持，此属性是必需的。

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

 

 





