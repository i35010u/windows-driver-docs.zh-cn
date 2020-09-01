---
title: KSCATEGORY_DATACOMPRESSOR
description: KSCATEGORY_DATACOMPRESSOR
ms.assetid: 7e4bf7b3-b3be-4a76-bc9e-0b1b020a7044
keywords:
- KSCATEGORY_DATACOMPRESSOR 设备和驱动程序安装
topic_type:
- apiref
api_name:
- KSCATEGORY_DATACOMPRESSOR
api_location:
- Ks.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: a45c8b7aff6f3c3711a72e143575272aea3155a2
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89097253"
---
# <a name="kscategory_datacompressor"></a>KSCATEGORY_DATACOMPRESSOR


KSCATEGORY_DATACOMPRESSOR [设备接口类](./overview-of-device-interface-classes.md) 是为用于压缩数据流的 [内核流式处理](../stream/streaming-minidrivers2.md) (KS) 功能类别定义的。

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
<td align="left"><p>KSCATEGORY_DATACOMPRESSOR</p></td>
</tr>
<tr class="even">
<td align="left"><p>类 GUID</p></td>
<td align="left"><p>{1E84C900-7E70-11D0-A5D6-28DB04C10000}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

KS 设备的驱动程序将注册 KSCATEGORY_DATACOMPRESSOR 的实例，以向操作系统指示设备支持 KSCATEGORY_DATACOMPRESSOR 功能类别。

KSCATEGORY_DATACOMPRESSOR 功能类别是 [**KSPROPERTY_TOPOLOGY_CATEGORIES**](../stream/ksproperty-topology-categories.md)之一。

有关为解压缩数据流的 KS 功能类别定义的设备接口类的信息，请参阅 [**KSCATEGORY_DATADECOMPRESSOR**](kscategory-datadecompressor.md)。

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


[**KSCATEGORY_DATADECOMPRESSOR**](kscategory-datadecompressor.md)

[**KSPROPERTY_TOPOLOGY_CATEGORIES**](../stream/ksproperty-topology-categories.md)

 

