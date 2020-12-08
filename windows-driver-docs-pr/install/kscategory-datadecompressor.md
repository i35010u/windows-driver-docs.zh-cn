---
title: KSCATEGORY_DATADECOMPRESSOR
description: KSCATEGORY_DATADECOMPRESSOR
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
ms.openlocfilehash: f58b13b2d867d7a5fdb970dc05b5a2b2c0f0498e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96829903"
---
# <a name="kscategory_datadecompressor"></a>KSCATEGORY_DATADECOMPRESSOR


KSCATEGORY_DATADECOMPRESSOR [设备接口类](./overview-of-device-interface-classes.md) 是为解压数据流 (KS) 功能类别定义的 [内核流式处理](../stream/streaming-minidrivers2.md) 的。

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

KS 设备的驱动程序将注册 KSCATEGORY_DATADECOMPRESSOR 的实例，以向操作系统指示设备支持 KSCATEGORY_DATADECOMPRESSOR 功能类别。

KSCATEGORY_DATADECOMPRESSOR 功能类别是 [**KSPROPERTY_TOPOLOGY_CATEGORIES**](../stream/ksproperty-topology-categories.md)之一。

有关为用于压缩数据流的 KS 功能类别定义的设备接口类的信息，请参阅 [**KSCATEGORY_DATACOMPRESSOR**](kscategory-datacompressor.md)。

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


[**KSCATEGORY_DATACOMPRESSOR**](kscategory-datacompressor.md)

[**KSPROPERTY_TOPOLOGY_CATEGORIES**](../stream/ksproperty-topology-categories.md)

 

