---
title: WIA\_IPS\_已启用\_修补\_代码\_类型
description: WIA\_IPS\_已启用\_修补\_代码\_类型属性用于选择为其修补程序代码读取器将搜索当前会话中的已启用修补程序代码。
ms.assetid: 278C93EF-661E-41B2-8882-DF05A2FB9723
keywords:
- WIA_IPS_ENABLED_PATCH_CODE_TYPES 成像设备
topic_type:
- apiref
api_name:
- WIA_IPS_ENABLED_PATCH_CODE_TYPES
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 89e9612720111b0c14109bb880dbb8ddd5c94355
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542859"
---
# <a name="wiaipsenabledpatchcodetypes"></a>WIA\_IPS\_已启用\_修补\_代码\_类型


**WIA\_IPS\_已启用\_修补\_代码\_类型**属性用于选择为其修补程序代码读取器将在当前搜索的已启用修补程序代码会话。 这些修补程序代码可以报告与 WIA 微型驱动程序的部分或全部使用值[ **WIA\_IPS\_支持\_PATCH\_代码\_类型**](wia-ips-supported-patch-code-types.md). 数组中值的顺序指定的优先级顺序为用要搜索的相应修补程序代码。




属性类型：VT\_I4 | VT\_VECTOR

有效值：WIA\_PROP\_NONE （单一 array / 矢量值）

访问权限：读/写

<a name="remarks"></a>备注
-------

有效值**WIA\_IP\_已启用\_修补\_代码\_类型**属性是相同的 WIA\_PATCH\_代码\_定义为值[ **WIA\_IP\_支持\_修补\_代码\_类型**](wia-ips-supported-patch-code-types.md)属性。

此属性是必需的修补程序代码读取器的所有项。

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

 

 





