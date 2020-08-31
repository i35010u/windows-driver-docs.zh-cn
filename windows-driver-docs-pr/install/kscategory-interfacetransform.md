---
title: KSCATEGORY_INTERFACETRANSFORM
description: KSCATEGORY_INTERFACETRANSFORM
ms.assetid: a33b5de9-6b51-41a6-bb06-392e1438f0cc
keywords:
- KSCATEGORY_INTERFACETRANSFORM 设备和驱动程序安装
topic_type:
- apiref
api_name:
- KSCATEGORY_INTERFACETRANSFORM
api_location:
- Ks.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 75b2a6df4cf222ef0e9a8a0851ba80c033b30690
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89095013"
---
# <a name="kscategory_interfacetransform"></a>KSCATEGORY_INTERFACETRANSFORM


为转换设备接口的[内核流式处理](../stream/streaming-minidrivers2.md) (KS) 功能类别定义 KSCATEGORY_INTERFACETRANSFORM[设备接口类](./overview-of-device-interface-classes.md)。

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
<td align="left"><p>KSCATEGORY_INTERFACETRANSFORM</p></td>
</tr>
<tr class="even">
<td align="left"><p>类 GUID</p></td>
<td align="left"><p>{CF1DDA2D-9743-11D0-A3EE-00A0C9223196}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

KS 设备的驱动程序将注册 KSCATEGORY_INTERFACETRANSFORM 的实例，以向操作系统指示设备支持 KSCATEGORY_INTERFACETRANSFORM 功能类别。

KSCATEGORY_INTERFACETRANSFORM 功能类别是 [**KSPROPERTY_TOPOLOGY_CATEGORIES**](../stream/ksproperty-topology-categories.md) 功能类别之一。

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

 

