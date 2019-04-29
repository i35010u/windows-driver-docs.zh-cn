---
title: KSCATEGORY_COMMUNICATIONSTRANSFORM
description: KSCATEGORY_COMMUNICATIONSTRANSFORM
ms.assetid: a958c5a6-18a3-43e0-a6ac-84a879a981da
keywords:
- KSCATEGORY_COMMUNICATIONSTRANSFORM 设备和驱动程序安装
topic_type:
- apiref
api_name:
- KSCATEGORY_COMMUNICATIONSTRANSFORM
api_location:
- Ks.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 243e8237329d196b40c24f2f12e090ef2f412502
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63377307"
---
# <a name="kscategorycommunicationstransform"></a>KSCATEGORY_COMMUNICATIONSTRANSFORM


KSCATEGORY_COMMUNICATIONSTRANSFORM[设备接口类](https://msdn.microsoft.com/library/windows/hardware/ff541339)为定义[内核流式处理](https://msdn.microsoft.com/library/windows/hardware/ff568277)通信转换设备 (KS) 功能类别。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">特性</th>
<th align="left">设置</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>标识符</p></td>
<td align="left"><p>KSCATEGORY_COMMUNICATIONSTRANSFORM</p></td>
</tr>
<tr class="even">
<td align="left"><p>类 GUID</p></td>
<td align="left"><p>{CF1DDA2C-9743-11D0-A3EE-00A0C9223196}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

KS 设备的驱动程序注册 KSCATEGORY_COMMUNICATIONSTRANSFORM 向操作系统指示设备支持 KSCATEGORY_COMMUNICATIONSTRANSFORM 功能分类的实例。

KSCATEGORY_COMMUNICATIONSTRANSFORM 功能类别是之一[ **KSPROPERTY_TOPOLOGY_CATEGORIES**](https://msdn.microsoft.com/library/windows/hardware/ff565799)。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Ks.h （包括 Ks.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**KSPROPERTY_TOPOLOGY_CATEGORIES**](https://msdn.microsoft.com/library/windows/hardware/ff565799)

 

 






