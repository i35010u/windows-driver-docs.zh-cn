---
title: MB 微型端口驱动程序 INF 要求
description: MB 微型端口驱动程序 INF 要求
ms.assetid: 1f248e1c-7faf-4a11-a4c2-3c0e829e1583
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7bbef3c703f47c2b0859b730613cd5451278bd65
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63343313"
---
# <a name="mb-miniport-driver-inf-requirements"></a>MB 微型端口驱动程序 INF 要求


MB 微型端口驱动程序必须在其 INF 文件中具有以下条目：

```INF
*IfType  = 243; IF_TYPE_WWANPP 
*MediaType  = 9; <mark type="enumval">NdisMediumWirelessWan</mark> 
*PhysicalMediaType  = 8; NdisPhysicalMediumWirelessWan
EnableDhcp  = 0; Disable DHCP

;Entries to be put in add-registry-section for NdisMediumWirelessWan
HKR, Ndi\Interfaces, UpperRange, 0, "flpp4, flpp6"
HKR, Ndi\Interfaces, LowerRange, 0, "ppip"
```

除 UpperRange 和 LowerRange，前面的代码示例中所述的所有条目都应与关键字，如 AddReg 和 CopyFiles 的同一个 INF 部分下。 应置于 UpperRange 和 LowerRange[添加注册表部分](add-registry-sections-in-a-network-inf-file.md)的 INF 文件。

### <a href="" id="-iftype"></a>\*IfType

双模式设备可以指定这两个*IfType*以下表中的值：

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>说明</strong></p></td>
<td align="left"><p><strong>名称</strong></p></td>
<td align="left"><p><strong>IfType</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p>基于 GSM 的 MB 设备</p></td>
<td align="left"><p>IF_TYPE_WWANPP</p></td>
<td align="left"><p>243</p></td>
</tr>
<tr class="odd">
<td align="left"><p>基于 CDMA 的 MB 设备</p></td>
<td align="left"><p>IF_TYPE_WWANPP2</p></td>
<td align="left"><p>244</p></td>
</tr>
</tbody>
</table>

 

### <a href="" id="-mediatype"></a>\*MediaType

MB 微型端口驱动程序必须指定一个从下表中的媒体类型值基于数据包分帧微型端口驱动程序能够解释在其发送和接收数据路径的类型。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>说明</strong></p></td>
<td align="left"><p><strong>名称</strong></p></td>
<td align="left"><p><strong>MediaType</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p>解释 802.3 数据包的 MB 微型端口驱动程序必须报告此媒体类型。 此框架仅适用于迁移旧的微型端口驱动程序并不建议用于生产质量微型端口驱动程序。</p></td>
<td align="left"><p>NdisMedium802_3</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="odd">
<td align="left"><p>MB 能够处理原始 IP 流量的微型端口驱动程序必须设置此媒体类型。 这是要在生产质量微型端口驱动程序中使用的建议的媒体类型。</p></td>
<td align="left"><p>NdisMediumWirelessWan</p></td>
<td align="left"><p>9</p></td>
</tr>
</tbody>
</table>

 

### <a name="enabledhcp"></a>EnableDhcp

MB 微型端口驱动程序必须指定从下表基于它们是否实现 DHCP 服务器仿真 EnableDhcp 值之一。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>值</strong></p></td>
<td align="left"><p><strong>说明</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p>0</p></td>
<td align="left"><p>为此接口上禁用 DHCP。 微型端口驱动程序未实现 DHCP 服务器欺骗。 这是要在生产品质的驱动程序中使用的建议的值。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>1</p></td>
<td align="left"><p>为此接口启用 DHCP。 微型端口驱动程序实现 DHCP 服务器欺骗。 也就是说，微型端口驱动程序将需要欺骗 DHCP 服务器和 ARP 解决方法。</p></td>
</tr>
</tbody>
</table>

 

### <a name="upperrange"></a>UpperRange

媒体类型为 NdisMediumWirelessWan 时，此关键字设置具有一个或多个以下的字符串 （如果适用） 的组合。 NdisMedium802\_3 种微型端口驱动程序应在 UpperRange 中使用的现有值。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>值</strong></p></td>
<td align="left"><p><strong>说明</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p>"flpp4"</p></td>
<td align="left"><p>微型端口驱动程序指定"flpp4"如果 MB 设备支持 IPv4。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>"flpp6"</p></td>
<td align="left"><p>微型端口驱动程序指定"flpp6"如果 MB 设备支持 IPv6。 仅适用于支持 IPv6 的设备需要此值。</p></td>
</tr>
</tbody>
</table>

 

### <a name="lowerrange"></a>LowerRange

此关键字必须最小值，NdisMediumWirelessWan 媒体类型时，以下的值。 NdisMedium802\_3 种微型端口驱动程序应在 LowerRange 中使用的现有值。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>值</strong></p></td>
<td align="left"><p><strong>说明</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p>"ppip"</p></td>
<td align="left"><p>在下边缘的 MB 设备类型。</p></td>
</tr>
</tbody>
</table>

 

 

 





