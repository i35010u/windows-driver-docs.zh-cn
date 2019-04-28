---
title: WIA\_IPS\_转移\_扫描\_底部
description: WIA\_IPS\_转移\_扫描\_以及 WIA 的下边缘属性\_IP\_通过\_扫描\_TOP，WIA\_IP\_转移\_扫描\_左侧和 WIA\_IPS\_转移\_扫描\_直接用于通过扫描英寸为单位的千分之几秒中配置的量 (0.001 \ 0034;)单元，相对于物理文档。
ms.assetid: 301BDAF1-6B6B-4C83-8B9F-A4B56DFF868B
keywords:
- WIA_IPS_OVER_SCAN_BOTTOM 成像设备
topic_type:
- apiref
api_name:
- WIA_IPS_OVER_SCAN_BOTTOM
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 05/22/2018
ms.localizationpriority: medium
ms.openlocfilehash: c761b5396ad739958cda29bfd69c0ebeb15164c6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63348200"
---
# <a name="wiaipsoverscanbottom"></a>WIA\_IPS\_转移\_扫描\_底部


**WIA\_IPS\_转移\_扫描\_底部**属性连同[ **WIA\_IP\_通过\_扫描\_顶部**](wia-ips-over-scan-top.md)， [ **WIA\_IP\_通过\_扫描\_左侧**](wia-ips-over-scan-left.md)，和[**WIA\_IPS\_转移\_扫描\_右**](wia-ips-over-scan-right.md)用于通过扫描，千分之一英寸 （0.001 英寸） 单元中相对于配置的量物理文档。 WIA 微型驱动程序创建并维护此属性。




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

 

 





