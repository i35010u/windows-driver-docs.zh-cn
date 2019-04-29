---
title: WIA\_IPS\_已启用\_条形码\_类型
description: WIA\_IPS\_已启用\_条形码\_类型属性用于选择已启用的条形码条码读取器将在当前会话中为其进行搜索。
ms.assetid: 7CB9FE6D-5E22-48ED-B948-01CC906CA46D
keywords:
- WIA_IPS_ENABLED_BARCODE_TYPES 成像设备
topic_type:
- apiref
api_name:
- WIA_IPS_ENABLED_BARCODE_TYPES
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1aba889669e07288e39425e96ddb00caa31ac378
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63370774"
---
# <a name="wiaipsenabledbarcodetypes"></a>WIA\_IPS\_已启用\_条形码\_类型


**WIA\_IPS\_已启用\_条形码\_类型**属性用于选择已启用的条形码条码读取器将在当前会话中为其进行搜索。 这些条形码可以报告与 WIA 微型驱动程序的部分或全部使用值[ **WIA\_IPS\_支持\_条形码\_类型**](wia-ips-supported-barcode-types.md)。 数组中值的顺序指定的优先级顺序为用要搜索相应的条形码。




属性类型：VT\_I4 | VT\_VECTOR

有效值：WIA\_PROP\_NONE （单一 array / 矢量值）

访问权限：读/写

<a name="remarks"></a>备注
-------

有效值**WIA\_IPS\_已启用\_条形码\_类型**属性是相同的 WIA\_条形码\_为定义的值[**WIA\_IPS\_支持\_条形码\_类型**](wia-ips-supported-barcode-types.md)属性。

此属性是必需的所有条码读取器项。

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

 

 





