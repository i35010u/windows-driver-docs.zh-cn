---
title: MB 微型端口驱动程序 INF 要求
description: MB 微型端口驱动程序 INF 要求
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1f98991337a4e13c7099cad3117377afa4f35809
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96791415"
---
# <a name="mb-miniport-driver-inf-requirements"></a>MB 微型端口驱动程序 INF 要求


MB 微型端口驱动程序必须在其 INF 文件中包含以下项：

```INF
*IfType  = 243; IF_TYPE_WWANPP 
*MediaType  = 9; <mark type="enumval">NdisMediumWirelessWan</mark> 
*PhysicalMediaType  = 8; NdisPhysicalMediumWirelessWan
EnableDhcp  = 0; Disable DHCP

;Entries to be put in add-registry-section for NdisMediumWirelessWan
HKR, Ndi\Interfaces, UpperRange, 0, "flpp4, flpp6"
HKR, Ndi\Interfaces, LowerRange, 0, "ppip"
```

前面的代码示例中所述的所有项（UpperRange 和 LowerRange 除外）应与关键字（如 AddReg 和 CopyFiles）相同的 INF 部分。 UpperRange 和 LowerRange 应放在 INF 文件的 " [添加注册表" 部分](add-registry-sections-in-a-network-inf-file.md) 中。

### <a name="iftype"></a><a href="" id="-iftype"></a>\*IfType

双模式设备可以指定下表中的 *IfType* 值之一：

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>描述</strong></p></td>
<td align="left"><p><strong>Name</strong></p></td>
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

 

### <a name="mediatype"></a><a href="" id="-mediatype"></a>\*MediaType

MB 微型端口驱动程序必须根据小型端口驱动程序可以在其发送和接收数据路径中解释的数据包组帧的类型，指定下表中的媒体类型值之一。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>描述</strong></p></td>
<td align="left"><p><strong>Name</strong></p></td>
<td align="left"><p><strong>MediaType</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p>解释802.3 数据包的 MB 微型端口驱动程序必须报告此媒体类型。 此框架仅用于迁移旧的微型端口驱动程序，不建议用于生产质量的微型端口驱动程序。</p></td>
<td align="left"><p>NdisMedium802_3</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="odd">
<td align="left"><p>可以处理原始 IP 流量的 MB 微型端口驱动程序必须设置此媒体类型。 这是建议用于生产质量微型端口驱动程序的媒体类型。</p></td>
<td align="left"><p>NdisMediumWirelessWan</p></td>
<td align="left"><p>9</p></td>
</tr>
</tbody>
</table>

 

### <a name="enabledhcp"></a>EnableDhcp

MB 微型端口驱动程序必须根据是否实现 DHCP 服务器模拟来指定下表中的 EnableDhcp 值之一。

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
<td align="left"><p>禁用此接口的 DHCP。 微型端口驱动程序未实现 DHCP 服务器欺骗。 这是在生产质量的驱动程序中使用的建议值。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>1</p></td>
<td align="left"><p>为此接口启用 DHCP。 微型端口驱动程序实现 DHCP 服务器欺骗。 也就是说，微型端口驱动程序将需要欺骗 DHCP 服务器和 ARP 解析。</p></td>
</tr>
</tbody>
</table>

 

### <a name="upperrange"></a>UpperRange

当媒体类型为 NdisMediumWirelessWan 时，此关键字设置为适用于以下字符串的一个或多个组合。 NdisMedium802 \_ 3 微型端口驱动程序应使用 UpperRange 中的现有值。

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
<td align="left"><p>如果 MB 设备支持 IPv4，则微型端口驱动程序指定 "flpp4"。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>"flpp6"</p></td>
<td align="left"><p>如果 MB 设备支持 IPv6，则微型端口驱动程序指定 "flpp6"。 仅支持 IPv6 的设备需要此值。</p></td>
</tr>
</tbody>
</table>

 

### <a name="lowerrange"></a>LowerRange

当 media 类型为 NdisMediumWirelessWan 时，此关键字的值必须至少为以下值。 NdisMedium802 \_ 3 微型端口驱动程序应使用 LowerRange 中的现有值。

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
<td align="left"><p>MB 设备类型。</p></td>
</tr>
</tbody>
</table>

 

 

 





