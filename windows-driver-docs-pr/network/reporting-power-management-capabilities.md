---
title: 报告电源管理功能
description: 报告电源管理功能
ms.assetid: cfacd885-e18a-44a5-939d-88e62b573ace
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e6ec12acb865f4933bcac3dca00039301b56c651
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842041"
---
# <a name="reporting-power-management-capabilities"></a>报告电源管理功能





支持 NDIS 6.20 和更高版本的 NDIS 驱动程序在初始化期间报告其硬件电源管理功能。 在绑定操作过程中，NDIS 会报告当前功能，以覆盖过量的 NDIS 协议驱动程序。 但是，NDIS 可以隐藏协议驱动程序中的某些功能。 例如，当用户禁用部分或全部电源管理功能时，NDIS 可能会报告不同的功能。

请注意，NDIS 向协议驱动程序报告的当前电源管理功能并不一定与微型端口驱动程序报告给 NDIS 的硬件功能相同。

如果 NDIS 6.1 或更低的微型端口驱动程序绑定到 NDIS 6.20 协议驱动程序，NDIS 会将电源管理功能转换为 NDIS 6.20 协议驱动程序支持的格式。 NDIS 还翻译了电源管理功能，NDIS 6.20 微型端口驱动程序将其报告为 NDIS 6.1 和更低版本的驱动程序支持的格式。

可在 INF 文件设置中启用或禁用微型端口驱动程序报告的硬件功能。 有关电源管理 INF 文件设置的详细信息，请参阅[电源管理的标准化 INF 关键字](standardized-inf-keywords-for-power-management.md)。

在微型端口初始化期间，微型端口驱动程序使用基础硬件的电源管理功能初始化[**NDIS\_PM\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_capabilities)结构。 微型端口驱动程序将[**ndis\_微型端口\_适配器**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)的**PowerManagementCapabilitiesEx**成员设置为指向**ndis\_PM\_功能**\_常规\_属性结构构造.

[**NDIS\_PM\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_capabilities)结构包含以下信息：

**随意**  
对于 NDIS 6.20，此成员是为 NDIS 保留的。

从 NDIS 6.30 开始，定义了以下标志：

<a href="" id="ndis-pm-wake-packet-indication-supported"></a>NDIS\_PM\_唤醒\_数据包\_支持指示\_  
如果设置了此标志，网络适配器可以保存收到的数据包，该数据包导致适配器生成唤醒事件。

有关此电源管理功能的详细信息，请参阅[NDIS 唤醒原因状态指示](ndis-wake-reason-status-indications.md)。

<a href="" id="ndis-pm-selective-suspend-supported"></a>\_选择性\_挂起\_支持 NDIS\_PM  
如果设置了此标志，则微型端口驱动程序对网络适配器支持 NDIS 选择性挂起。

有关此电源管理功能的详细信息，请参阅 " [NDIS 选择性挂起](ndis-selective-suspend.md)"。

<a href="" id="supportedwolpacketpatterns"></a>**SupportedWoLPacketPatterns**  
包含指定网络适配器支持的 LAN 唤醒（WOL）数据包模式的标志。 例如，网络适配器在收到位图、WOL 幻数据包或 EAP over LAN （EAPOL）请求标识符消息时，可以生成唤醒事件。 有关当前操作系统中支持的模式的完整列表，请参阅[**NDIS\_PM\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_capabilities)参考 "页。

<a href="" id="numtotalwolpatterns"></a>**NumTotalWoLPatterns**  
一个**ULONG**值，其中包含网络适配器支持的 WOL 模式的总数。 这是 "支持的 WOL 协议模式数量" 和 "支持的 WOL 位图模式的数量" 之和。

例如，如果驱动程序支持8种灵活的位图模式、IPv4 TCP SYN （通过预设筛选器）和幻数据包，则会在 NumTotalWoLPatterns 中报告9。 （8个位图 + 1 个 IPv4 TCP SYN = 9）

**请注意**  WOL 模式的总数不包括 "幻数据包唤醒模式"。

 

有关 WOL 协议模式的详细信息，请参阅[**NDIS\_PM\_WOL\_模式**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_wol_pattern)。

<a href="" id="maxwolpatternsize"></a>**MaxWoLPatternSize**  
包含可与模式进行比较的最大字节数。

<a href="" id="maxwolpatternoffset"></a>**MaxWoLPatternOffset**  
包含可检查的数据包中的字节数，从 MAC 标头的开头开始。

<a href="" id="maxwolpacketsavebuffer"></a>**MaxWoLPacketSaveBuffer**  
包含一个多端口驱动程序可以保存到缓冲区并指示驱动程序堆栈的 WOL 协议模式的字节数。

<a href="" id="supportedprotocoloffloads"></a>**SupportedProtocolOffloads**  
包含一些标志，这些标志指定网络适配器支持的电源管理协议卸载功能。 微型端口驱动程序使用这些标志报告网络适配器的低功率协议卸载功能。 例如，网络适配器可以支持 IPv4 ARP 卸载、IPv6 邻居请求（NS）或 IEEE 802.11 稳健安全网络（RSN）4路和双向握手。 有关当前操作系统中支持的协议卸载的完整列表，请参阅[**NDIS\_PM\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_capabilities)参考 "页。

<a href="" id="numarpoffloadipv4addresses"></a>**NumArpOffloadIPv4Addresses**  
包含 ARP 卸载 IPv4 地址的数目。

<a href="" id="numnsoffloadipv6addresses"></a>**NumNSOffloadIPv6Addresses**  
包含网络适配器支持的卸载 IPv6 请求数。

<a href="" id="minmagicpacketwakeup"></a>**MinMagicPacketWakeUp**  
指定网络适配器可用于在收到*幻数据包*时发出唤醒事件信号的最小设备电源状态。 （*幻数据包*是包含接收网络适配器的以太网地址的16个连续副本的数据包。）

<a href="" id="minpatternwakeup"></a>**MinPatternWakeUp**  
指定网络适配器在收到包含由协议驱动程序指定的模式的网络帧时，可用于发出唤醒事件的最小设备电源状态。

<a href="" id="minlinkchangewakeup"></a>**MinLinkChangeWakeUp**  
指定在发生链接更改（媒体连接或断开连接）时网络适配器可用于发出唤醒事件信号的最小设备电源状态。

<a href="" id="supportedwakeupevents"></a>**SupportedWakeUpEvents**  
指定网络适配器所支持的与媒体无关的唤醒事件。 这些事件不特定于媒体类型。 例如，这些唤醒事件包含链接更改事件。

<a href="" id="mediaspecificwakeupevents"></a>**MediaSpecificWakeUpEvents**  
指定网络适配器支持的特定于媒体的唤醒事件。 例如，以下事件包括：

-   802.11 网络适配器与访问点（AP）解除了。

-   移动宽带（MB）网络适配器将其注册状态更改检测到 MB 服务。

如果微型端口驱动程序支持将协议卸载到处于低功耗状态的网络适配器，则该驱动程序必须支持对模式匹配 WOL 事件所支持的协议卸载使用相同的低功耗状态;也就是说，在**MinPatternWakeUp**或**MinMagicPacketWakeUp**成员中指定的值。

NDIS 使用基础网络适配器当前可用的电源管理功能初始化[**ndis\_PM\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_capabilities)结构，并在绑定操作过程中向其传递协议过量协议驱动程序。 NDIS 将[**ndis\_绑定\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_bind_parameters)结构的**PowerManagementCapabilitiesEx**成员设置为指向 NDIS\_PM\_功能结构。

过量驱动程序可以使用[oid\_PM\_硬件\_功能](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pm-hardware-capabilities)OID 查询来获取网络适配器的硬件电源管理功能。 NDIS 代表微型端口驱动程序处理此 OID 请求。 \_硬件\_功能 OID 请求支持 OID\_PM，则不需要 NDIS 微型端口驱动程序。

过量驱动程序可以使用[oid\_PM\_当前\_功能](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pm-current-capabilities)OID 来查询网络适配器当前可用的电源管理功能。 NDIS 代表微型端口驱动程序处理此 OID 请求。 \_PM\_当前\_功能 OID 请求，不需要 NDIS 微型端口驱动程序。

 

 





