---
title: KSCATEGORY_FILESYSTEM
description: KSCATEGORY_FILESYSTEM
ms.assetid: a3d6a3dc-926a-415a-80ef-c7d2f11ed4bf
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
ms.openlocfilehash: 41d5062a35b42ab02fbbb1e49557ee1e9023c1c5
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89097241"
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

## <a name="see-also"></a>另请参阅


[**KSPROPERTY_TOPOLOGY_CATEGORIES**](../stream/ksproperty-topology-categories.md)

 

