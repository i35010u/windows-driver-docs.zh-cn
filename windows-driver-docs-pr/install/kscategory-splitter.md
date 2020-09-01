---
title: KSCATEGORY_SPLITTER
description: KSCATEGORY_SPLITTER
ms.assetid: 056b6bc0-5566-4498-959d-dbc9725aa03e
keywords:
- KSCATEGORY_SPLITTER 设备和驱动程序安装
topic_type:
- apiref
api_name:
- KSCATEGORY_SPLITTER
api_location:
- Ks.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 754c106d092684fb6214cb8face4fb9f10ee8096
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89096007"
---
# <a name="kscategory_splitter"></a>KSCATEGORY_SPLITTER


为拆分数据流的[内核流式处理](../stream/streaming-minidrivers2.md) (KS) 功能类别定义 KSCATEGORY_SPLITTER[设备接口类](./overview-of-device-interface-classes.md)。

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
<td align="left"><p>KSCATEGORY_SPLITTER</p></td>
</tr>
<tr class="even">
<td align="left"><p>类 GUID</p></td>
<td align="left"><p>{0A4252A0-7E70-11D0-A5D6-28DB04C10000}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

适用于 KS 音频适配器设备的驱动程序注册一个 KSCATEGORY_SPLITTER 实例，以向操作系统指示设备支持 KSCATEGORY_SPLITTER 功能类别。

KSCATEGORY_SPLITTER 功能类别是 [**KSPROPERTY_TOPOLOGY_CATEGORIES**](../stream/ksproperty-topology-categories.md) 功能类别之一。

有关拆分器的一般信息，请参阅 [AVStream 拆分](../stream/avstream-splitters.md)器。

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

 

