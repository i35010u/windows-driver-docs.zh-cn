---
title: MB 适配器常规属性要求
description: MB 适配器常规属性要求
ms.assetid: c2bfb625-3455-41e0-abdd-ab7204eaae0a
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 183dd81a4bfb7e5c9383e0cabc4e740cffcb4f45
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63343455"
---
# <a name="mb-adapter-general-attribute-requirements"></a>MB 适配器常规属性要求


下表描述了微型端口驱动程序应设置该成员的变量的值[ **NDIS\_微型端口\_适配器\_常规\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff565923)结构。 MB 微型端口驱动程序必须使用这些值，当它们调用[ **NdisMSetMiniportAttributes** ](https://msdn.microsoft.com/library/windows/hardware/ff563672)从其[ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)在微型端口驱动程序初始化过程中的函数。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">INF 文件中的字段</th>
<th align="left">建议的值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>IfType</p></td>
<td align="left"><p>基于 GSM 的设备必须指定 IF_TYPE_WWANPP。</p>
<p>基于 CDMA 的设备指定 IF_TYPE_WWANPP2。</p>
<p>值必须匹配 * IfType 微型端口驱动程序的 INF 文件中指定的值。</p></td>
</tr>
<tr class="even">
<td align="left"><p>MediaType</p></td>
<td align="left"><p>值必须匹配 * 微型端口驱动程序的 INF 文件中指定的媒体类型值。 例如，可以<strong>NdisMediumWirelessWan</strong>或<strong>NdisMedium802_3</strong>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>PhysicalMediumType</p></td>
<td align="left"><p>值必须匹配 * PhysicalMediaType 微型端口驱动程序的 INF 文件中指定的值。 该值必须是<strong>NdisPhysicalMediumWirelessWan</strong>。</p></td>
</tr>
<tr class="even">
<td align="left"><p>AccessType</p></td>
<td align="left"><p>如果媒体类型中的值指定为<strong>NdisMediumWirelessWan</strong>，指定<strong>NET_IF_ACCESS_POINT_TO_POINT</strong> AccessType 的。 如果 MediaType <strong>NdisMedium802_3</strong>，指定 NET_IF_ACCESS_BROADCAST。</p></td>
</tr>
</tbody>
</table>

 

 

 





