---
title: WIA\_IPS\_最大\_条形码\_搜索\_重试
description: WIA\_IPS\_最大\_条形码\_搜索\_重试次数属性描述了如果可以启用条形码检测时找到没有条形码读取器会尝试的重试的最大数目。
ms.assetid: AA9255D2-6B3B-4539-8C9C-7B0B84E2417D
keywords:
- WIA_IPS_MAXIMUM_BARCODE_SEARCH_RETRIES 成像设备
topic_type:
- apiref
api_name:
- WIA_IPS_MAXIMUM_BARCODE_SEARCH_RETRIES
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 05/22/2018
ms.localizationpriority: medium
ms.openlocfilehash: 08cf90984ff258a20fc061c04d6cf78d65d415ec
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56563086"
---
# <a name="wiaipsmaximumbarcodesearchretries"></a>WIA\_IPS\_最大\_条形码\_搜索\_重试


**WIA\_IPS\_最大\_条形码\_搜索\_重试**属性描述的最大重试，如果没有条形码可以找到时，会尝试读取器数条形码检测已启用。



属性类型：VT\_UI4

有效值：WIA\_PROP\_RANGE

访问权限：读/写

<a name="remarks"></a>备注
-------

此属性是必需的所有条码读取器项。 若要支持的范围为包含单个值，包括 0 （不重试），可以实现属性。

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

 

 





