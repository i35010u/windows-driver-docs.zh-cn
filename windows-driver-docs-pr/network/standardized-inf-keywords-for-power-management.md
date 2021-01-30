---
title: 电源管理的标准化 INF 关键字
description: 电源管理的标准化 INF 关键字
ms.date: 01/29/2021
ms.localizationpriority: medium
ms.custom: contperf-fy21q3
ms.openlocfilehash: ed2af65371ea571c64461c2ca5714aca92e40f7d
ms.sourcegitcommit: 597ef5dc63565202a8c6d9e51c9faf1b6398968a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/29/2021
ms.locfileid: "99081111"
---
# <a name="standardized-inf-keywords-for-power-management"></a>电源管理的标准化 INF 关键字

电源管理标准化关键字在设备驱动程序 INF 文件中定义。 操作系统将读取这些标准化关键字，并调整设备的当前电源管理功能。 

[网络适配器 WDF 类扩展 (NetAdapterCx) ](../netcx/index.md)客户端驱动程序和传统的 NDIS 微型端口设备驱动程序都使用这些电源管理关键字。 但是，有些关键字只是由 NetAdapterCx 驱动程序使用，而另一些则由 NDIS 驱动程序专门使用，如以下部分所述：

* [NetAdapterCx 和 NDIS 的电源管理关键字](#power-management-keywords-for-netadaptercx-and-ndis)

* [电源管理关键字专用于 NetAdapterCx](#power-management-keywords-exclusive-to-netadaptercx)

* [用于 NDIS 的电源管理关键字](#power-management-keywords-exclusive-to-ndis)

传统 NDIS 微型端口设备驱动程序应始终在 [**ndis \_ 微型端口适配器的 " \_ \_ 常规 \_ 属性**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes) " 结构中指出设备的硬件电源管理功能。

 

有关标准化 INF 关键字的详细信息，请参阅 [网络设备的标准化 Inf 关键字](standardized-inf-keywords-for-network-devices.md)。

## <a name="power-management-keywords-for-netadaptercx-and-ndis"></a>NetAdapterCx 和 NDIS 的电源管理关键字

定义了以下标准化 INF 关键字，以启用或禁用对网络适配器电源管理功能的支持。 它们由 NetAdapterCx 客户端驱动程序和传统的 NDIS 微型端口设备驱动程序使用。

<a href="" id="-wakeonpattern"></a>**\*WakeOnPattern**  
一个值，该值描述当网络数据包与指定的模式匹配时是否应启用设备来唤醒计算机。

<a href="" id="-wakeonmagicpacket"></a>**\*WakeOnMagicPacket**  
一个值，用于描述在设备接收到 *幻数据包* 时是否应启用设备来唤醒计算机。  (*幻数据包* 是包含接收网络适配器的以太网地址的16个连续副本的数据包) 

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

<a href="" id="value"></a>值  
与列表中的每个选项关联的枚举整数值。 此值存储在 **NDI \\ params \\**<em>SubkeyName 值中 \\ 。</em>

<a href="" id="enumdesc"></a>EnumDesc  
与菜单中显示的每个值相关联的显示文本。

下表描述了 NDIS 和 NetAdapterCx 驱动程序所使用的电源管理关键字的可能 INF 条目。


|SubkeyName|ParamDesc|值|EnumDesc|
|--- |--- |--- |--- |
|**_WakeOnPattern_**|模式匹配时唤醒|0|已禁用|
|||1 (默认值) |已启用|
|**WakeOnMagicPacket**|幻数据包唤醒|0|已禁用|
|||1 (默认值) |已启用|
|**PMARPOffload**|ARP 卸载|0|已禁用|
|||1 (默认值) |已启用|
|**_PMNSOffload_**|NS 卸载|0|已禁用|
|||1 (默认值) |已启用|
|**PMWiFiRekeyOffload**|WiFi 重新生成密钥卸载|0|已禁用|
|||1 (默认值) |已启用|
|**_EEE_*|Energy-Efficient 以太网|0|已禁用|
|||1 (默认值) |已启用|

## <a name="power-management-keywords-exclusive-to-netadaptercx"></a>电源管理关键字专用于 NetAdapterCx

以下电源管理关键字仅适用于 NetAdapterCx 客户端驱动程序的使用。 

除了允许用户控制设备空闲和唤醒行为中所述的设备空闲和唤醒行为的标准 WDF 进程 [外，NetAdapterCx](../wdf/user-control-of-device-idle-and-wake-behavior.md)还定义了网络设备特定的标准化 INF 关键字，以允许更多控制。

**\*IdleRestriction**  
如果网络设备处于空闲关机状态并唤醒数据包筛选器功能，则此设置允许用户确定设备空闲关机的时间。

**\* IdleRestriction** 是一个枚举标准化 INF 关键字，具有以下属性：

下表描述了 **\* IdleRestriction** 关键字的可能 INF 条目。

|SubkeyName|ParamDesc|值|EnumDesc|
|--- |--- |--- |--- |
|**_*IdleRestriction_**|空闲关机限制|0（默认值）|无限制|
|||1|仅当用户不存在时空闲|


## <a name="power-management-keywords-exclusive-to-ndis"></a>用于 NDIS 的电源管理关键字

以下电源管理关键字仅适用于传统的 NDIS 微型端口驱动程序。 NetAdapterCx 客户端驱动程序不得使用它们。

<a href="" id="-modernstandbywolmagicpacket"></a>**\*ModernStandbyWoLMagicPacket**  
一个值，用于描述在设备接收到 *幻 paket* 并且系统处于 *S0ix* 电源状态时是否应启用设备唤醒计算机。 当系统处于 *S4* 电源状态时，此功能不适用。

> [!NOTE]
> 在 NDIS 6.60 和更高版本，或者 Windows 10 版本1607及更高版本中支持 **\* ModernStandbyWoLMagicPacket** 。 

<a href="" id="-devicesleepondisconnect"></a>**\*DeviceSleepOnDisconnect**  
一个值，该值描述当媒体断开连接时，是否应启用设备以将设备置于低功耗状态 (睡眠状态) ，并在媒体再次连接时恢复 (唤醒) 状态。

下表描述了 NDIS 微型端口驱动程序所使用的电源管理关键字的可能 INF 条目。

|SubkeyName|ParamDesc|值|EnumDesc|
|--- |--- |--- |--- |
|**ModernStandbyWoLMagicPacket**|当系统处于 _S0ix_ 电源状态时唤醒幻数据包|0（默认值）|已禁用|
|||1|已启用|
|**_DeviceSleepOnDisconnect_**|断开连接时设备睡眠|0|已禁用|
|||1 (默认值) |已启用|
 

