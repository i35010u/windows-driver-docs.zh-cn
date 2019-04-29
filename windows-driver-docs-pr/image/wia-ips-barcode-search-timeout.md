---
title: WIA\_IPS\_条形码\_搜索\_超时
description: WIA\_IPS\_条形码\_搜索\_超时属性描述要搜索的文档页上的条形码时遇到的最长时间。
ms.assetid: 3EE6C492-722E-439A-8BB5-03496DAC78D2
keywords:
- WIA_IPS_BARCODE_SEARCH_TIMEOUT 成像设备
topic_type:
- apiref
api_name:
- WIA_IPS_BARCODE_SEARCH_TIMEOUT
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 05/22/2018
ms.localizationpriority: medium
ms.openlocfilehash: df86fce0ce3ceeebd250349b52365058ba270d8f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63370635"
---
# <a name="wiaipsbarcodesearchtimeout"></a>WIA\_IPS\_条形码\_搜索\_超时


**WIA\_IPS\_条形码\_搜索\_超时**属性描述要搜索的文档页上的条形码时遇到的最长时间。


属性类型：VT\_UI4

有效值：WIA\_PROP\_RANGE

访问权限：读/写

<a name="remarks"></a>备注
-------

未指定时间单位 （它可以是毫秒或秒的十分之几例如），但应用程序可以选择值中最小值-最大范围内报告的 WIA 微型驱动程序。

此属性是必需的所有条码读取器项。 可以实现属性支持包含一个 （这意味着应用程序不能更改此超时值） 的单个值的范围。

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

 

 





