---
title: WIA\_IPS\_MAXIMUM\_PATCH\_CODE\_SEARCH\_RETRIES
description: WIA\_IPS\_最大\_修补\_代码\_搜索\_重试次数属性描述最大数目的重试，如果没有修补程序可以找到代码时，读取器会尝试修补代码启用检测。
ms.assetid: F6CBEC7E-B44D-4524-9F75-8CBF413FCAF6
keywords:
- WIA_IPS_MAXIMUM_PATCH_CODE_SEARCH_RETRIES 成像设备
topic_type:
- apiref
api_name:
- WIA_IPS_MAXIMUM_PATCH_CODE_SEARCH_RETRIES
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9c29eb0244089fc7c51f7c5856febb5575a57fa1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56533273"
---
# <a name="wiaipsmaximumpatchcodesearchretries"></a>WIA\_IPS\_MAXIMUM\_PATCH\_CODE\_SEARCH\_RETRIES


**WIA\_IPS\_最大\_修补\_代码\_搜索\_重试**属性描述了如果没有读取器会尝试的重试的最大数目启用修补程序代码检测时，可以找到修补程序代码。




属性类型：VT\_I4

有效值：WIA\_PROP\_RANGE

访问权限：读/写

<a name="remarks"></a>备注
-------

此属性是必需的修补程序代码读取器的所有项。 若要支持的范围为包含单个值，包括 0 （不重试），可以实现属性。

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

 

 





