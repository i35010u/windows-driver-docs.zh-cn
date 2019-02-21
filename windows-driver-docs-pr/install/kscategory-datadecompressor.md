---
title: KSCATEGORY_DATADECOMPRESSOR
description: KSCATEGORY_DATADECOMPRESSOR
ms.assetid: 260906fc-fdd5-487f-9f45-db6ca4591233
keywords:
- KSCATEGORY_DATADECOMPRESSOR 设备和驱动程序安装
topic_type:
- apiref
api_name:
- KSCATEGORY_DATADECOMPRESSOR
api_location:
- Ks.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: b67117f9a9f75071c12f3819fbd4ed8d806c5f11
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56546134"
---
# <a name="kscategorydatadecompressor"></a>KSCATEGORY_DATADECOMPRESSOR


KSCATEGORY_DATADECOMPRESSOR[设备接口类](https://msdn.microsoft.com/library/windows/hardware/ff541339)为定义[内核流式处理](https://msdn.microsoft.com/library/windows/hardware/ff568277)解压缩的数据流的 (KS) 功能类别。

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
<td align="left"><p>KSCATEGORY_DATADECOMPRESSOR</p></td>
</tr>
<tr class="even">
<td align="left"><p>类 GUID</p></td>
<td align="left"><p>{2721AE20-7E70-11D0-A5D6-28DB04C10000}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

KS 设备的驱动程序注册 KSCATEGORY_DATADECOMPRESSOR 向操作系统指示设备支持 KSCATEGORY_DATADECOMPRESSOR 功能分类的实例。

KSCATEGORY_DATADECOMPRESSOR 功能类别是之一[ **KSPROPERTY_TOPOLOGY_CATEGORIES**](https://msdn.microsoft.com/library/windows/hardware/ff565799)。

有关为压缩数据流的 KS 功能类别定义的设备接口类的信息，请参阅[ **KSCATEGORY_DATACOMPRESSOR**](kscategory-datacompressor.md)。

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


[**KSCATEGORY_DATACOMPRESSOR**](kscategory-datacompressor.md)

[**KSPROPERTY_TOPOLOGY_CATEGORIES**](https://msdn.microsoft.com/library/windows/hardware/ff565799)

 

 






