---
title: KSCATEGORY_MEDIUMTRANSFORM
description: KSCATEGORY_MEDIUMTRANSFORM
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
ms.openlocfilehash: fb01d7fc54978bfb51834434584edb98da257426
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96795471"
---
# <a name="kscategory_mediumtransform"></a>KSCATEGORY_MEDIUMTRANSFORM


KSCATEGORY_MEDIUMTRANSFORM [设备接口类](./overview-of-device-interface-classes.md) 为 [内核流式处理](../stream/streaming-minidrivers2.md) (KS) 功能类别定义，转换正在使用的媒体类型。

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

KS 设备的驱动程序将注册 KSCATEGORY_MEDIUMTRANSFORM 的实例，以向操作系统指示设备支持 KSCATEGORY_MEDIUMTRANSFORM 功能类别。

KSCATEGORY_MEDIUMTRANSFORM 功能类别是 [**KSPROPERTY_TOPOLOGY_CATEGORIES**](../stream/ksproperty-topology-categories.md) 功能类别之一。

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

 

