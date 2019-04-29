---
title: 电源管理的标准化 INF 关键字
description: 电源管理的标准化 INF 关键字
ms.assetid: bec8dd96-f64a-40eb-ade9-73c9a66a756e
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d9e7789589b24256aa2efdff9836b12d3c2df9b4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390665"
---
# <a name="standardized-inf-keywords-for-power-management"></a>电源管理的标准化 INF 关键字





设备驱动程序 INF 文件中定义的电源管理进行了标准化关键字。 操作系统读取这些标准化的关键字并调整设备的当前电源管理功能。 设备驱动程序应始终指示到 NDIS 中设备的硬件电源管理功能[ **NDIS\_微型端口\_适配器\_常规\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff565923)结构。

以下的标准化的 INF 关键字定义来启用或禁用对电源管理功能的网络适配器的支持。

<a href="" id="-wakeonpattern"></a>**\*WakeOnPattern**  
描述是否应启用设备唤醒计算机时的网络数据包与指定的模式匹配的值。

<a href="" id="-wakeonmagicpacket"></a>**\*WakeOnMagicPacket**  
一个值，描述是否应启用设备唤醒计算机时，设备收到*幻数据包*。 (A*幻数据包*是包含 16 个连续副本接收的网络适配器的以太网地址的数据包)

<a href="" id="-devicesleepondisconnect"></a>**\*DeviceSleepOnDisconnect**  
描述是否应启用该设备将设备置于低功耗状态 （睡眠状态） 的值在媒体是断开连接并且返回到全功率状态 （唤醒状态） 媒体时重新连接。

<a href="" id="-pmarpoffload"></a>**\*PMARPOffload**  
一个值，描述是否应启用设备卸载地址解析协议 (ARP)，当系统进入睡眠状态。

<a href="" id="-pmnsoffload"></a>**\*PMNSOffload**  
一个值，描述是否应启用设备卸载邻居请求 (NS)，当系统进入睡眠状态。

<a href="" id="-pmwifirekeyoffload"></a>**\*PMWiFiRekeyOffload**  
一个值，描述是否应启用设备卸载组临时键 (GTK) 上无线的 LAN 唤醒 (WOL) 的计算机进入睡眠状态时重新生成的密钥。

<a href="" id="-eee"></a>**\*EEE**  
一个值，描述该设备是否应启用 IEEE 802.3az 能效较高的以太网。

本主题末尾处表中的列描述枚举关键字的以下属性：

<a href="" id="subkeyname"></a>SubkeyName  
必须指定 INF 文件中的关键字的名称显示在注册表中。

<a href="" id="paramdesc"></a>ParamDesc  
显示文本与 SubkeyName 相关联。

<a href="" id="value"></a>值  
在列表中每个选项与关联枚举的整数值。 此值存储在**NDI\\params\\**<em>SubkeyName\\值。</em>

<a href="" id="enumdesc"></a>EnumDesc  
与每个菜单中显示的值相关联的显示文本。

下表描述了可能的电源管理关键字的 INF 项。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">SubkeyName</th>
<th align="left">ParamDesc</th>
<th align="left">ReplTest1</th>
<th align="left">EnumDesc</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong><em>WakeOnPattern</strong></p></td>
<td align="left"><p>唤醒模式匹配</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>Disabled</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1 （默认值）</p></td>
<td align="left"><p>Enabled</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong></em>WakeOnMagicPacket</strong></p></td>
<td align="left"><p>项的幻数据包唤醒</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>Disabled</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1 （默认值）</p></td>
<td align="left"><p>Enabled</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><em>DeviceSleepOnDisconnect</strong></p></td>
<td align="left"><p>设备上的睡眠断开连接</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>Disabled</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1 （默认值）</p></td>
<td align="left"><p>Enabled</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong></em>PMARPOffload</strong></p></td>
<td align="left"><p>ARP 卸载</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>Disabled</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1 （默认值）</p></td>
<td align="left"><p>Enabled</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><em>PMNSOffload</strong></p></td>
<td align="left"><p>NS 卸载</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>Disabled</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1 （默认值）</p></td>
<td align="left"><p>Enabled</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong></em>PMWiFiRekeyOffload</strong></p></td>
<td align="left"><p>WiFi 重新生成密钥卸载</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>Disabled</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1 （默认值）</p></td>
<td align="left"><p>Enabled</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>*EEE</strong></p></td>
<td align="left"><p>能效较高的以太网</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>Disabled</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1 （默认值）</p></td>
<td align="left"><p>Enabled</p></td>
</tr>
</tbody>
</table>

 

有关标准化 INF 关键字的详细信息，请参阅[为网络设备的标准化 INF 关键字](standardized-inf-keywords-for-network-devices.md)。

 

 





