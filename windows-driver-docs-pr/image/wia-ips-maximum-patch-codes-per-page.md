---
title: WIA\_IPS\_MAXIMUM\_PATCH\_CODES\_PER\_PAGE
description: WIA\_IPS\_最大\_修补\_代码\_每\_页属性在一个文档页端描述设备可以并应该会检测到的修补程序代码的最大数目时启用了修补程序代码检测。
ms.assetid: 91A0DAC0-D8F3-48BB-9DD4-AF50BD8F09AB
keywords:
- WIA_IPS_MAXIMUM_PATCH_CODES_PER_PAGE 成像设备
topic_type:
- apiref
api_name:
- WIA_IPS_MAXIMUM_PATCH_CODES_PER_PAGE
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 413b47d857d390f4b7a345368785b32f79d5fae9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541253"
---
# <a name="wiaipsmaximumpatchcodesperpage"></a>WIA\_IPS\_MAXIMUM\_PATCH\_CODES\_PER\_PAGE


**WIA\_IPS\_最大\_修补\_代码\_每\_页**属性描述的修补程序代码的设备可以并且应该最大数目检测一个文档页端上启用修补程序代码检测。




属性类型：VT\_I4

有效值：WIA\_PROP\_RANGE

访问权限：读/写

<a name="remarks"></a>备注
-------

值为 0 表示"无最大值"。 应用程序可以减少此属性的当前值，以减少修补程序代码检测所用的时间并提高扫描速度。

此属性是必需的修补程序代码读取器的所有项，但它可作为包含仅为 0 （最小值等于最大值和设置为 0，步骤大小为 0） 值的范围容器。

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

 

 





