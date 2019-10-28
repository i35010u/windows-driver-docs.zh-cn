---
title: MB 适配器常规属性要求
description: MB 适配器常规属性要求
ms.assetid: c2bfb625-3455-41e0-abdd-ab7204eaae0a
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 25f6aef763437311a8721f37bb5564df007c23e0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844300"
---
# <a name="mb-adapter-general-attribute-requirements"></a>MB 适配器常规属性要求


下表描述了微型端口驱动程序应将[**NDIS\_微型端口\_\_适配器**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)的成员变量设置为的常规\_属性结构的值。 当微型端口驱动程序初始化期间，MB 微型端口驱动程序必须使用这些值来从其[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)函数调用[**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes) 。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">INF 文件中的字段</th>
<th align="left">建议值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>IfType</p></td>
<td align="left"><p>基于 GSM 的设备必须指定 IF_TYPE_WWANPP。</p>
<p>基于 CDMA 的设备指定 IF_TYPE_WWANPP2。</p>
<p>该值必须与微型端口驱动程序的 INF 文件中指定的 * IfType 值匹配。</p></td>
</tr>
<tr class="even">
<td align="left"><p>MediaType</p></td>
<td align="left"><p>该值必须与微型端口驱动程序的 INF 文件中指定的 * 媒体的值匹配。 例如， <strong>NdisMediumWirelessWan</strong>或<strong>NdisMedium802_3</strong>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>PhysicalMediumType</p></td>
<td align="left"><p>该值必须与微型端口驱动程序的 INF 文件中指定的 * PhysicalMediaType 值匹配。 该值必须为<strong>NdisPhysicalMediumWirelessWan</strong>。</p></td>
</tr>
<tr class="even">
<td align="left"><p>AccessType</p></td>
<td align="left"><p>如果 "媒体" 中的值指定为<strong>NdisMediumWirelessWan</strong>，则为 AccessType 指定<strong>NET_IF_ACCESS_POINT_TO_POINT</strong> 。 如果媒体<strong>NdisMedium802_3</strong>，请指定 NET_IF_ACCESS_BROADCAST。</p></td>
</tr>
</tbody>
</table>

 

 

 





