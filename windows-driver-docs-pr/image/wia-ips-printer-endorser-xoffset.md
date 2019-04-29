---
title: WIA\_IPS\_打印机\_印记签署器\_拼音
description: WIA\_IPS\_打印机\_印记签署器\_拼音属性用于在一英寸的千分之几秒中配置的水平坐标 (0.001 \ 0034;)，认可 imprinting/区域的左上角的相对于要进行扫描的物理文档的左上角和印刷/认可中。 WIA 微型驱动程序创建并维护此属性。
ms.assetid: 3B3E1A02-0401-455C-B341-37FBEB108E4F
keywords:
- WIA_IPS_PRINTER_ENDORSER_XOFFSET 成像设备
topic_type:
- apiref
api_name:
- WIA_IPS_PRINTER_ENDORSER_XOFFSET
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 05/22/2018
ms.localizationpriority: medium
ms.openlocfilehash: 969c7ecbf3b3aa50f5102ec371a4054cdf0ef728
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391107"
---
# <a name="wiaipsprinterendorserxoffset"></a>WIA\_IPS\_打印机\_印记签署器\_拼音


**WIA\_IPS\_打印机\_印记签署器\_拼音**属性用于配置的水平坐标中的一英寸 （0.001"），千分之几秒的左上角认可 imprinting/区域，相对于物理要扫描的文档和印刷/认可的左上角。 WIA 微型驱动程序创建并维护此属性。




属性类型：VT\_UI4

有效值：WIA\_PROP\_RANGE

访问权限：读/写

<a name="remarks"></a>备注
-------

WIA 微型驱动程序可以更新值和当前值的有效范围 （如果它变得超出范围） 到最接近的可用位置时[ **WIA\_IPS\_打印机\_印记签署器**](wia-ips-printer-endorser.md)属性 （即，从到送纸器平板） 更改为新的特定输入源。

此属性是可选的所有印刷器/印记签署器数据源项。

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

 

 





