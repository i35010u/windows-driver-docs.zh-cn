---
title: KSCATEGORY_BRIDGE
description: KSCATEGORY_BRIDGE
ms.assetid: 7973cac5-2b74-4af1-8912-370e922e5f4d
keywords:
- KSCATEGORY_BRIDGE 设备和驱动程序安装
topic_type:
- apiref
api_name:
- KSCATEGORY_BRIDGE
api_location:
- Ks.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: bc3fef53c7bf069ce37102e4801b9b6a8e7ff743
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63377311"
---
# <a name="kscategorybridge"></a>KSCATEGORY_BRIDGE


KSCATEGORY_BRIDGE[设备接口类](https://msdn.microsoft.com/library/windows/hardware/ff541339)为定义[内核流式处理](https://msdn.microsoft.com/library/windows/hardware/ff568277)(KS) 支持软件接口 KS 子系统和另一个软件之间的功能类别组件。

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
<td align="left"><p>KSCATEGORY_BRIDGE</p></td>
</tr>
<tr class="even">
<td align="left"><p>类 GUID</p></td>
<td align="left"><p>{085AFF00-62CE-11CF-A5D6-28DB04C10000}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

KS 音频适配器设备驱动程序注册 KSCATEGORY_BRIDGE 向操作系统指示设备支持 KSCATEGORY_BRIDGE 功能分类的实例。

有关 KSCATEGORY_BRIDGE 功能类别的详细信息，请参阅[ **KSPROPERTY_TOPOLOGY_CATEGORIES**](https://msdn.microsoft.com/library/windows/hardware/ff565799)。

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

 

 





