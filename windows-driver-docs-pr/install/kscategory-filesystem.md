---
title: KSCATEGORY_FILESYSTEM
description: KSCATEGORY_FILESYSTEM
keywords:
- KSCATEGORY_FILESYSTEM 设备和驱动程序安装
topic_type:
- apiref
api_name:
- KSCATEGORY_FILESYSTEM
api_location:
- Ks.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 13964a5b43778f41887b5894203182ea139e62c5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96795481"
---
# <a name="kscategory_filesystem"></a>KSCATEGORY_FILESYSTEM


KSCATEGORY_FILESYSTEM [设备接口类](./overview-of-device-interface-classes.md) 定义为 [内核流式处理](../stream/streaming-minidrivers2.md) (KS) 功能类别，该类别将数据流移入或移出文件系统。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Attribute</th>
<th align="left">设置</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>标识符</p></td>
<td align="left"><p>KSCATEGORY_FILESYSTEM</p></td>
</tr>
<tr class="even">
<td align="left"><p>类 GUID</p></td>
<td align="left"><p>{760FED5E-9357-11D0-A3CC-00A0C9223196}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

KS 设备的驱动程序将注册 KSCATEGORY_FILESYSTEM 的实例，以向操作系统指示设备支持 KSCATEGORY_FILESYSTEM 功能类别。

KSCATEGORY_FILESYSTEM 功能类别是 [**KSPROPERTY_TOPOLOGY_CATEGORIES**](../stream/ksproperty-topology-categories.md) 功能类别之一。

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
<td align="left">Ks (包含 Ks .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**KSPROPERTY_TOPOLOGY_CATEGORIES**](../stream/ksproperty-topology-categories.md)

 

