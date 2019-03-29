---
title: KSCATEGORY_MEDIUMTRANSFORM
description: KSCATEGORY_MEDIUMTRANSFORM
ms.assetid: a57c0dd5-48b1-4f58-ac3a-e1f175a228f0
keywords:
- KSCATEGORY_MEDIUMTRANSFORM 设备和驱动程序安装
topic_type:
- apiref
api_name:
- KSCATEGORY_MEDIUMTRANSFORM
api_location:
- Ks.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: efbffb7af1d7f3e4370b0f81d3370b3428d6ba68
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566961"
---
# <a name="kscategorymediumtransform"></a>KSCATEGORY_MEDIUMTRANSFORM


KSCATEGORY_MEDIUMTRANSFORM[设备接口类](https://msdn.microsoft.com/library/windows/hardware/ff541339)为定义[内核流式处理](https://msdn.microsoft.com/library/windows/hardware/ff568277)(KS) 转换的正在使用的介质的类型的功能类别。

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
<td align="left"><p>KSCATEGORY_MEDIUMTRANSFORM</p></td>
</tr>
<tr class="even">
<td align="left"><p>类 GUID</p></td>
<td align="left"><p>{CF1DDA2E-9743-11D0-A3EE-00A0C9223196}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

KS 设备的驱动程序注册 KSCATEGORY_MEDIUMTRANSFORM 向操作系统指示设备支持 KSCATEGORY_MEDIUMTRANSFORM 功能分类的实例。

KSCATEGORY_MEDIUMTRANSFORM 功能类别是之一[ **KSPROPERTY_TOPOLOGY_CATEGORIES** ](https://msdn.microsoft.com/library/windows/hardware/ff565799)功能类别。

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

 

 






