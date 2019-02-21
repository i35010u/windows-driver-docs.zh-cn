---
title: WIA\_IPS\_修补\_代码\_搜索\_超时
description: WIA\_IPS\_修补\_代码\_搜索\_超时属性描述要搜索的文档页上的修补程序代码的最长时间。
ms.assetid: D7DD05B2-43CA-484F-8207-4ED9C307D3AA
keywords:
- WIA_IPS_PATCH_CODE_SEARCH_TIMEOUT 成像设备
topic_type:
- apiref
api_name:
- WIA_IPS_PATCH_CODE_SEARCH_TIMEOUT
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: baf882dd97c4cad00df3e3f6debb08b9d8cb2980
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521888"
---
# <a name="wiaipspatchcodesearchtimeout"></a>WIA\_IPS\_修补\_代码\_搜索\_超时


**WIA\_IPS\_修补\_代码\_搜索\_超时**属性描述要搜索的文档页上的修补程序代码的最长时间。




属性类型：VT\_I4

有效值：WIA\_PROP\_RANGE

访问权限：读/写

<a name="remarks"></a>备注
-------

未指定时间单位 （它可以是毫秒或秒的十分之几秒例如），但应用程序可以选择值中最小值-最大范围内报告的 WIA 微型驱动程序。

此属性是必需的修补程序代码读取器的所有项。 此属性可以实现支持范围包含一个单一值 （这意味着应用程序不能更改此超时）

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

 

 





