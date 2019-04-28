---
title: WIA\_IPS\_打印机\_印记签署器\_正文
description: WIA\_IPS\_打印机\_印记签署器\_正文属性用于配置算的垂直坐标，以英寸为单位的千分之几秒 (0.001 \ 0034;)，认可 imprinting/区域的左上角的相对于要进行扫描的物理文档的左上角和印刷/认可中。 WIA 微型驱动程序创建并维护此属性。
ms.assetid: C04A4EAC-237A-44D6-AB05-CD561DA72CE8
keywords:
- WIA_IPS_PRINTER_ENDORSER_YOFFSET 成像设备
topic_type:
- apiref
api_name:
- WIA_IPS_PRINTER_ENDORSER_YOFFSET
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 05/22/2018
ms.localizationpriority: medium
ms.openlocfilehash: 1e873d5c7b8dedb085479e9a3ae7ac5b6f3542e0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63353321"
---
# <a name="wiaipsprinterendorseryoffset"></a>WIA\_IPS\_打印机\_印记签署器\_正文


**WIA\_IPS\_打印机\_印记签署器\_正文**属性用于配置的垂直坐标中的一英寸 （0.001"），千分之几秒的左上角认可 imprinting/区域，相对于物理要扫描的文档和印刷/认可的左上角。 WIA 微型驱动程序创建并维护此属性。




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

 

 





