---
title: KSCATEGORY_TOPOLOGY
description: KSCATEGORY_TOPOLOGY
ms.assetid: 20c4ccf1-81bb-4209-9842-4de295fe3a00
keywords:
- KSCATEGORY_TOPOLOGY 设备和驱动程序安装
topic_type:
- apiref
api_name:
- KSCATEGORY_TOPOLOGY
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 7a5281b4b74a83a99af0b153b85041ee49c782a8
ms.sourcegitcommit: e6d80e33042e15d7f2b2d9868d25d07b927c86a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/05/2020
ms.locfileid: "91733493"
---
# <a name="kscategory_topology"></a>KSCATEGORY_TOPOLOGY


对于音频设备的内部拓扑，为[内核流式处理](../stream/streaming-minidrivers2.md) (KS) 功能类别定义 KSCATEGORY_TOPOLOGY[设备接口类](./overview-of-device-interface-classes.md)。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">属性</th>
<th align="left">设置</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>标识符</p></td>
<td align="left"><p>KSCATEGORY_TOPOLOGY</p></td>
</tr>
<tr class="even">
<td align="left"><p>类 GUID</p></td>
<td align="left"><p>{DDA54A40-1E4C-11D1-A050-405705C10000}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

适用于 KS 音频适配器设备的驱动程序将 KSCATEGORY_TOPOLOGY 的实例注册，以指示操作系统设备支持 KSCATEGORY_TOPOLOGY 功能类别。

有关音频适配器的设备接口类的信息，请参阅 [安装音频适配器的设备接口](../audio/installing-device-interfaces-for-an-audio-adapter.md)。

在 WDK 中提供的 [交流电 "97 示例驱动程序](/samples/browse/) " 枚举 KSCATEGORY_TOPOLOGY 设备接口类的实例。

WDK 中的 sysfx 示例将注册此设备接口类的实例。 Sysfx 示例位于 WDK 的 *src \\ 音频 \\ sysfx 目录* 中。

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

