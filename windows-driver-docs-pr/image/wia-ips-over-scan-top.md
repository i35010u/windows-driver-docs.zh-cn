---
title: WIA\_IPS\_转移\_扫描\_顶部
description: WIA\_IP\_转移\_扫描\_TOP 属性以及 WIA\_IP\_通过\_扫描\_下边框、 WIA\_IP\_转移\_扫描\_左侧和 WIA\_IPS\_转移\_扫描\_直接用于通过扫描英寸为单位的千分之几秒中配置的量 (0.001 \ 0034;)单元，相对于物理文档。
ms.assetid: 7957BBB4-C4E6-4704-A64D-F2F318ABDF61
keywords:
- WIA_IPS_OVER_SCAN_TOP 成像设备
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
ms.openlocfilehash: 977b4a1933e1627e26176f009ec027bb4eebd97d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56545039"
---
# <a name="wiaipsoverscantop"></a>WIA\_IPS\_转移\_扫描\_顶部


**WIA\_IPS\_转移\_扫描\_顶部**属性连同[ **WIA\_IP\_通过\_扫描\_底部**](wia-ips-over-scan-bottom.md)， [ **WIA\_IP\_通过\_扫描\_左侧**](wia-ips-over-scan-left.md)，和[**WIA\_IPS\_转移\_扫描\_右**](wia-ips-over-scan-right.md)用于通过扫描，千分之一英寸 （0.001 英寸） 单元中相对于配置的量物理文档。 WIA 微型驱动程序创建并维护此属性。




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
<td><p>标头</p></td>
<td>Wiadef.h （包括 Wiadef.h）</td>
</tr>
</tbody>
</table>

 

 





