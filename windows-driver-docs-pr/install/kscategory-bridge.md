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
ms.openlocfilehash: a226efdddf45335d0c2da862819755f562355845
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89097263"
---
# <a name="kscategory_bridge"></a>KSCATEGORY_BRIDGE


KSCATEGORY_BRIDGE [设备接口类](./overview-of-device-interface-classes.md) 是为 [内核流式处理](../stream/streaming-minidrivers2.md) (KS) 功能类别定义的，它支持 KS 子系统与其他软件组件之间的软件接口。

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

适用于 KS 音频适配器设备的驱动程序将 KSCATEGORY_BRIDGE 的实例注册，以指示操作系统设备支持 KSCATEGORY_BRIDGE 功能类别。

有关 KSCATEGORY_BRIDGE 功能类别的详细信息，请参阅 [**KSPROPERTY_TOPOLOGY_CATEGORIES**](../stream/ksproperty-topology-categories.md)。

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

 

