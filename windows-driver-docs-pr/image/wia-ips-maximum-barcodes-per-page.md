---
title: WIA\_IPS\_MAXIMUM\_BARCODES\_PER\_PAGE
description: WIA\_IPS\_最大\_条形码\_每\_页属性在启用条形码检测上一个文档页端描述条形码，设备可以并应该会检测到的最大数目.
ms.assetid: 9DA59D24-3483-4663-8B6A-54EC53A3466D
keywords:
- WIA_IPS_MAXIMUM_BARCODES_PER_PAGE 成像设备
topic_type:
- apiref
api_name:
- WIA_IPS_MAXIMUM_BARCODES_PER_PAGE
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 05/22/2018
ms.localizationpriority: medium
ms.openlocfilehash: cbf8b863d500a9c39593ecb8b39777a1983d6da7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56563451"
---
# <a name="wiaipsmaximumbarcodesperpage"></a>WIA\_IPS\_MAXIMUM\_BARCODES\_PER\_PAGE


**WIA\_IPS\_最大\_条形码\_每\_页**属性上一个文档描述的设备可以并应该检测条形码时遇到的最大数目页端启用条形码检测。




属性类型：VT\_UI4

有效值：WIA\_PROP\_RANGE

访问权限：读/写

<a name="remarks"></a>备注
-------

值为 0 表示"无最大值。" 应用程序可以减少此属性的当前值，以减少条形码检测所用的时间并提高扫描速度。

此属性是必需的所有条码读取器项，但它可作为包含仅为 0 （最小值等于最大值和设置为 0，步骤大小为 0） 值的范围容器。

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

 

 





