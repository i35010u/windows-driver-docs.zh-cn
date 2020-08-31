---
title: KSCATEGORY_MULTIPLEXER
description: KSCATEGORY_MULTIPLEXER
ms.assetid: 3023769a-9b98-4c12-90b1-f83294a45ab0
keywords:
- KSCATEGORY_MULTIPLEXER 设备和驱动程序安装
topic_type:
- apiref
api_name:
- KSCATEGORY_MULTIPLEXER
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 1051af1a1f4d69d27ff61c9fc17128baab025e13
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89095679"
---
# <a name="kscategory_multiplexer"></a>KSCATEGORY_MULTIPLEXER


为多路复用器设备的[内核流式处理](../stream/streaming-minidrivers2.md) (KS) 功能类别定义 KSCATEGORY_MULTIPLEXER[设备接口类](./overview-of-device-interface-classes.md)。

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
<td align="left"><p>KSCATEGORY_MULTIPLEXER</p></td>
</tr>
<tr class="even">
<td align="left"><p>类 GUID</p></td>
<td align="left"><p>{7A5DE1D3-01A1-452c-B481-4FA2B96271E8}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

KS 设备的驱动程序将注册 KSCATEGORY_MULTIPLEXER 的实例，以向操作系统指示设备支持 KSCATEGORY_MULTIPLEXER 功能类别。

有关如何在 INF 文件中注册此功能类别的示例，请参阅 WDK 的*src/swtuner/algtuner*目录中的软件调谐器示例附带的*Bdan* inf 文件。

有关 multiplexers (的信息，请参阅 [拓扑筛选器](../audio/topology-filters.md)。

有关 KSCATEGORY_MULTIPLEXER 功能类别的详细信息，请参阅 [编码器安装和注册](../stream/encoder-installation-and-registration.md)。

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
<td align="left">Ksmedia (包含 Ksmedia) </td>
</tr>
</tbody>
</table>

 

