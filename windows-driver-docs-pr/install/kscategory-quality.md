---
title: KSCATEGORY_QUALITY
description: KSCATEGORY_QUALITY
ms.assetid: fc23e069-b514-41a3-b3c2-c65b35b2e431
keywords:
- KSCATEGORY_QUALITY 设备和驱动程序安装
topic_type:
- apiref
api_name:
- KSCATEGORY_QUALITY
api_location:
- Ks.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 4f784e0a606f10bd2c92f3cc6ccf5cf62f8150e6
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89095061"
---
# <a name="kscategory_quality"></a>KSCATEGORY_QUALITY


KSCATEGORY_QUALITY [设备接口类](./overview-of-device-interface-classes.md) 定义用于质量管理的 [内核流式处理](../stream/streaming-minidrivers2.md) (KS) 功能类别。

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
<td align="left"><p>KSCATEGORY_QUALITY</p></td>
</tr>
<tr class="even">
<td align="left"><p>类 GUID</p></td>
<td align="left"><p>{97EBAACB-95BD-11D0-A3EA-00A0C9223196}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

KS 设备的驱动程序将注册 KSCATEGORY_QUALITY 的实例，以向操作系统指示设备支持 KSCATEGORY_QUALITY 功能类别。

有关详细信息，请参阅 [质量管理](../stream/quality-management.md)。

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

 

