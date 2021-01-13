---
title: 电源管理的标准化 INF 关键字
description: 电源管理的标准化 INF 关键字
ms.date: 08/01/2019
ms.localizationpriority: medium
ms.openlocfilehash: 3061aaa35d175be19c1dc71873ee219dc9cab402
ms.sourcegitcommit: 06453fd351dd272e7710dbe5c0c3a49ce4326957
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/13/2021
ms.locfileid: "98180237"
---
# <a name="standardized-inf-keywords-for-power-management"></a>电源管理的标准化 INF 关键字

电源管理标准化关键字在设备驱动程序 INF 文件中定义。 操作系统将读取这些标准化关键字，并调整设备的当前电源管理功能。 传统 NDIS 微型端口设备驱动程序应始终在 [**ndis \_ 微型端口适配器的 " \_ \_ 常规 \_ 属性**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes) " 结构中指出设备的硬件电源管理功能。

定义了以下标准化 INF 关键字，以启用或禁用对网络适配器电源管理功能的支持。

<a href="" id="-wakeonpattern"></a>**\*WakeOnPattern**  
一个值，该值描述当网络数据包与指定的模式匹配时是否应启用设备来唤醒计算机。

<a href="" id="-wakeonmagicpacket"></a>**\*WakeOnMagicPacket**  
一个值，用于描述在设备接收到 *幻数据包* 时是否应启用设备来唤醒计算机。  (*幻数据包* 是包含接收网络适配器的以太网地址的16个连续副本的数据包) 

<a href="" id="-modernstandbywolmagicpacket"></a>**\*ModernStandbyWoLMagicPacket**  
一个值，用于描述在设备接收到 *幻 paket* 并且系统处于 *S0ix* 电源状态时是否应启用设备唤醒计算机。 当系统处于 *S4* 电源状态时，此功能不适用。

> [!NOTE]
> 在 NDIS 6.60 和更高版本，或者 Windows 10 版本1607及更高版本中支持 **\* ModernStandbyWoLMagicPacket** 。 它仅适用于传统的 NDIS 微型端口驱动程序。

> [!NOTE]
> **\* ModernStandbyWoLMagicPacket** 在 [网络适配器 WDF 类扩展中已弃用 (NetAdapterCx)](../netcx/index.md) ，它的客户端驱动程序不得使用。

<a href="" id="-devicesleepondisconnect"></a>**\*DeviceSleepOnDisconnect**  
一个值，该值描述当媒体断开连接时，是否应启用设备以将设备置于低功耗状态 (睡眠状态) ，并在媒体再次连接时恢复 (唤醒) 状态。

> [!NOTE]
> **\* DeviceSleepOnDisconnect** 在 [网络适配器 WDF 类扩展中已弃用 (NetAdapterCx)](../netcx/index.md) ，它的客户端驱动程序不得使用。

<a href="" id="-pmarpoffload"></a>**\*PMARPOffload**  
一个值，该值描述当系统进入睡眠状态时是否应启用设备以将地址解析协议 (ARP) 卸载。

<a href="" id="-pmnsoffload"></a>**\*PMNSOffload**  
一个值，该值描述当系统进入睡眠状态时，是否应启用设备来卸载 (NS) 的邻居请求。

<a href="" id="-pmwifirekeyoffload"></a>**\*PMWiFiRekeyOffload**  
一个值，用于描述在计算机进入睡眠状态时，是否应启用设备 (，以便在计算机进入睡眠状态时，对 LAN 唤醒 (WOL) 进行) 重新加密。

<a href="" id="-eee"></a>**\*EEE**  
一个值，该值描述设备是否应启用 IEEE 802.3 az Energy-Efficient 以太网。

本主题末尾的表中的列描述了用于枚举关键字的以下属性：

<a href="" id="subkeyname"></a>SubkeyName  
必须在 INF 文件中指定并且出现在注册表中的关键字的名称。

<a href="" id="paramdesc"></a>ParamDesc  
与 SubkeyName 关联的显示文本。

<a href="" id="value"></a>Value  
与列表中的每个选项关联的枚举整数值。 此值存储在 **NDI \\ params \\**<em>SubkeyName 值中 \\ 。</em>

<a href="" id="enumdesc"></a>EnumDesc  
与菜单中显示的每个值相关联的显示文本。

下表描述了电源管理关键字的可能 INF 条目。

<table>  
<colgroup> <col width="25%" /> <col width="25%" /> <col width="25%" /> <col width="25%" /> </colgroup>  
<thead>  
<tr class="header">  
<th align="left">SubkeyName</th>
<th align="left">ParamDesc</th>
<th align="left">Value</th>
<th align="left">EnumDesc</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong><em>WakeOnPattern</strong></p></td>
<td align="left"><p>模式匹配时唤醒</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>已禁用</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1 (默认值) </p></td>
<td align="left"><p>启用</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong></em>WakeOnMagicPacket</strong></p></td>
<td align="left"><p>幻数据包唤醒</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>已禁用</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1 (默认值) </p></td>
<td align="left"><p>启用</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong></em>ModernStandbyWoLMagicPacket</strong></p></td>
<td align="left"><p>当系统处于 <i>S0ix</i> 电源状态时唤醒幻数据包</p></td>
<td align="left"><p>0（默认值）</p></td>
<td align="left"><p>禁用</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1</p></td>
<td align="left"><p>已启用</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><em>DeviceSleepOnDisconnect</strong></p></td>
<td align="left"><p>断开连接时设备睡眠</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>已禁用</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1 (默认值) </p></td>
<td align="left"><p>启用</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong></em>PMARPOffload</strong></p></td>
<td align="left"><p>ARP 卸载</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>已禁用</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1 (默认值) </p></td>
<td align="left"><p>启用</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><em>PMNSOffload</strong></p></td>
<td align="left"><p>NS 卸载</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>已禁用</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1 (默认值) </p></td>
<td align="left"><p>启用</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong></em>PMWiFiRekeyOffload</strong></p></td>
<td align="left"><p>WiFi 重新生成密钥卸载</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>已禁用</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1 (默认值) </p></td>
<td align="left"><p>启用</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>*EEE</strong></p></td>
<td align="left"><p>Energy-Efficient 以太网</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>已禁用</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1 (默认值) </p></td>
<td align="left"><p>启用</p></td>
</tr>
</tbody>
</table>

 

有关标准化 INF 关键字的详细信息，请参阅 [网络设备的标准化 Inf 关键字](standardized-inf-keywords-for-network-devices.md)。

 

