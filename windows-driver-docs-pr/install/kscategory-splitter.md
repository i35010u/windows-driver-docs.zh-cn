---
title: KSCATEGORY_SPLITTER
description: KSCATEGORY_SPLITTER
ms.assetid: 056b6bc0-5566-4498-959d-dbc9725aa03e
keywords:
- KSCATEGORY_SPLITTER 设备和驱动程序安装
topic_type:
- apiref
api_name:
- KSCATEGORY_SPLITTER
api_location:
- Ks.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: c82c6787948473707fc23e29fd927b56c2a3c0e6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526117"
---
# <a name="kscategorysplitter"></a>KSCATEGORY_SPLITTER


KSCATEGORY_SPLITTER[设备接口类](https://msdn.microsoft.com/library/windows/hardware/ff541339)为定义[内核流式处理](https://msdn.microsoft.com/library/windows/hardware/ff568277)(KS) 功能类别将拆分数据流。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">属性</th>
<th align="left">设置</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>标识符</p></td>
<td align="left"><p>KSCATEGORY_SPLITTER</p></td>
</tr>
<tr class="even">
<td align="left"><p>类 GUID</p></td>
<td align="left"><p>{0A4252A0-7E70-11D0-A5D6-28DB04C10000}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

KS 音频适配器设备驱动程序注册 KSCATEGORY_SPLITTER 向操作系统指示设备支持 KSCATEGORY_SPLITTER 功能分类的实例。

KSCATEGORY_SPLITTER 功能类别是之一[ **KSPROPERTY_TOPOLOGY_CATEGORIES** ](https://msdn.microsoft.com/library/windows/hardware/ff565799)功能类别。

有关拆分条中的常规信息，请参阅[AVStream 拆分条](https://msdn.microsoft.com/library/windows/hardware/ff554255)。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>标头</p></td>
<td align="left">Ks.h （包括 Ks.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**KSPROPERTY_TOPOLOGY_CATEGORIES**](https://msdn.microsoft.com/library/windows/hardware/ff565799)

 

 






