---
title: KSCATEGORY_CLOCK
description: KSCATEGORY_CLOCK
ms.assetid: 1a5afadd-f76f-4184-a93e-af82769ecc1b
keywords:
- KSCATEGORY_CLOCK 设备和驱动程序安装
topic_type:
- apiref
api_name:
- KSCATEGORY_CLOCK
api_location:
- Ks.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 4cc770e4647f0d62c51f1e6d82aa4dcaf995c8d1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526149"
---
# <a name="kscategoryclock"></a>KSCATEGORY_CLOCK


KSCATEGORY_CLOCK[设备接口类](https://msdn.microsoft.com/library/windows/hardware/ff541339)为定义[内核流式处理](https://msdn.microsoft.com/library/windows/hardware/ff568277)时钟设备 (KS) 功能类别。

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
<td align="left"><p>KSCATEGORY_CLOCK</p></td>
</tr>
<tr class="even">
<td align="left"><p>类 GUID</p></td>
<td align="left"><p>{53172480-4791-11D0-A5D6-28DB04C10000}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

KS 设备的驱动程序注册 KSCATEGORY_CLOCK 向操作系统指示设备支持 KSCATEGORY_CLOCK 功能分类的实例。

有关流式处理时钟的内核的详细信息，请参阅[KS 微型驱动程序体系结构](https://msdn.microsoft.com/library/windows/hardware/ff567656)， [KS 时钟](https://msdn.microsoft.com/library/windows/hardware/ff567307)，并[AVStream 时钟](https://msdn.microsoft.com/library/windows/hardware/ff554208)。

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

 

 





