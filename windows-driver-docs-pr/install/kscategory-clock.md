---
title: KSCATEGORY_CLOCK
description: KSCATEGORY_CLOCK
keywords:
- KSCATEGORY_CLOCK 设备和驱动程序安装
topic_type:
- apiref
api_name:
- KSCATEGORY_CLOCK
api_location:
- Ks.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: c468073cd7aae60d73217ed12911ea5dfecb7d61
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96829893"
---
# <a name="kscategory_clock"></a>KSCATEGORY_CLOCK


为时钟设备的[内核流式处理](../stream/streaming-minidrivers2.md) (KS) 功能类别定义 KSCATEGORY_CLOCK[设备接口类](./overview-of-device-interface-classes.md)。

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
<td align="left"><p>KSCATEGORY_CLOCK</p></td>
</tr>
<tr class="even">
<td align="left"><p>类 GUID</p></td>
<td align="left"><p>{53172480-4791-11D0-A5D6-28DB04C10000}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

KS 设备的驱动程序将注册 KSCATEGORY_CLOCK 的实例，以向操作系统指示设备支持 KSCATEGORY_CLOCK 功能类别。

有关内核流式处理时钟的详细信息，请参阅 [Ks 微型驱动程序体系结构](../stream/ks-minidriver-architecture.md)、 [Ks 时钟](../stream/ks-clocks.md)和 [AVStream 时钟](../stream/avstream-clocks.md)。

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

 

