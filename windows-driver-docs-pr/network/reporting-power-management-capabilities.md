---
title: 报告电源管理功能
description: 报告电源管理功能
ms.assetid: cfacd885-e18a-44a5-939d-88e62b573ace
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2060b7e8f6bbccb684f77e77719155cc350f92b8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523747"
---
# <a name="reporting-power-management-capabilities"></a>报告电源管理功能





支持 NDIS 6.20 和更高版本的 NDIS 的微型端口驱动程序在初始化期间报告其硬件电源管理功能。 NDIS 报告的当前功能，在绑定操作过程过量协议的 NDIS 驱动程序。 但是，NDIS 可以隐藏来自协议驱动程序的一些功能。 例如，NDIS 可能会报告不同的功能，当用户禁用部分或全部的电源管理功能。

请注意，NDIS 报告给协议驱动程序的当前电源管理功能不一定是到 NDIS 微型端口驱动程序报告的硬件功能相同。

如果 NDIS 6.1 或更早的微型端口驱动程序绑定到 NDIS 6.20 协议驱动程序，NDIS 将转换为 NDIS 6.20 协议驱动程序支持的格式的电源管理功能。 NDIS 也将转换成的 NDIS 6.1 和之前基础驱动程序支持的格式的 NDIS 6.20 微型端口驱动程序报告的电源管理功能。

可以启用或禁用 INF 文件设置中的微型端口驱动程序报告的硬件功能。 有关电源管理 INF 文件设置的详细信息，请参阅[电源管理的标准化 INF 关键字](standardized-inf-keywords-for-power-management.md)。

微型端口在初始化期间，微型端口驱动程序初始化[ **NDIS\_PM\_功能**](https://msdn.microsoft.com/library/windows/hardware/ff566748)与电源管理功能的基础结构硬件。 微型端口驱动程序集**PowerManagementCapabilitiesEx**的成员[ **NDIS\_微型端口\_适配器\_常规\_属性** ](https://msdn.microsoft.com/library/windows/hardware/ff565923)结构，以指向**NDIS\_PM\_功能**结构。

[ **NDIS\_PM\_功能**](https://msdn.microsoft.com/library/windows/hardware/ff566748)结构包括以下信息：

**标志**  
对于 NDIS 6.20 此成员是 ndis 保留。

从 NDIS 6.30 开始，定义以下标志：

<a href="" id="ndis-pm-wake-packet-indication-supported"></a>NDIS\_PM\_唤醒\_数据包\_指示\_支持  
如果设置此标志，网络适配器可以保存所接收的数据包，导致适配器以生成唤醒事件。

有关此电源管理功能的详细信息，请参阅[NDIS 唤醒原因状态指示](ndis-wake-reason-status-indications.md)。

<a href="" id="ndis-pm-selective-suspend-supported"></a>NDIS\_PM\_选择性\_挂起\_支持  
如果设置此标志，NDIS 选择性暂停的微型端口驱动程序支持的网络适配器。

有关此电源管理功能的详细信息，请参阅[NDIS 选择性挂起](ndis-selective-suspend.md)。

<a href="" id="supportedwolpacketpatterns"></a>**SupportedWoLPacketPatterns**  
包含指定的网络适配器支持的 LAN 唤醒 (WOL) 数据包模式的标志。 例如，网络适配器可以生成唤醒事件时接收通过 LAN (EAPOL) 请求标识符消息位图、 WOL 的幻数据包或 EAP。 在当前操作系统中支持的模式的完整列表，请参阅[ **NDIS\_PM\_功能**](https://msdn.microsoft.com/library/windows/hardware/ff566748)参考页。

<a href="" id="numtotalwolpatterns"></a>**NumTotalWoLPatterns**  
一个**ULONG**值，该值包含网络适配器支持的 WOL 模式的总数。 这是"的受支持的 WOL 协议模式数"和"的受支持的 WOL 位图模式的数。"的总和

例如，如果您的驱动程序支持 8 灵活的位图模式、 IPv4 TCP SYN （通过预设筛选器） 和的幻数据包，然后将报告 NumTotalWoLPatterns 第 9。 (8 位图 + 1 IPv4 TCP SYN = 9)

**请注意**  WOL 模式的总数不包括的幻数据包唤醒模式。

 

WOL 协议模式的详细信息，请参阅[ **NDIS\_PM\_WOL\_模式**](https://msdn.microsoft.com/library/windows/hardware/ff566768)。

<a href="" id="maxwolpatternsize"></a>**MaxWoLPatternSize**  
包含的最大可与一种模式进行比较的字节数。

<a href="" id="maxwolpatternoffset"></a>**MaxWoLPatternOffset**  
包含中的数据包，可以进行检查，这将启动从 MAC 标头的开始的字节数。

<a href="" id="maxwolpacketsavebuffer"></a>**MaxWoLPacketSaveBuffer**  
包含的 WOL 协议模式的微型端口驱动程序可以将保存到一个缓冲区，并指定驱动程序堆栈中向上的字节数。

<a href="" id="supportedprotocoloffloads"></a>**SupportedProtocolOffloads**  
包含指定的电源管理协议卸载网络适配器支持的功能标志。 微型端口驱动程序使用这些标志，以低能耗协议卸载网络适配器的功能的报表。 例如，网络适配器可以支持 IPv4 ARP 卸载、 IPv6 邻居招标 (NS) 或 IEEE 802.11 可靠安全的网络 (RSN) 4 路和 2 路握手。 在当前操作系统中支持协议卸载的完整列表，请参阅[ **NDIS\_PM\_功能**](https://msdn.microsoft.com/library/windows/hardware/ff566748)参考页。

<a href="" id="numarpoffloadipv4addresses"></a>**NumArpOffloadIPv4Addresses**  
包含 IPv4 地址的 ARP 卸载数。

<a href="" id="numnsoffloadipv6addresses"></a>**NumNSOffloadIPv6Addresses**  
包含网络请求 (NS) 卸载的网络适配器支持 IPv6 请求数。

<a href="" id="minmagicpacketwakeup"></a>**MinMagicPacketWakeUp**  
指定从其网络适配器可以发出信号的回执上的唤醒事件的最低设备电源状态*幻数据包*。 (A*幻数据包*是包含 16 个连续副本接收的网络适配器的以太网地址的数据包。)

<a href="" id="minpatternwakeup"></a>**MinPatternWakeUp**  
指定从其网络适配器，可以发出接收包含由协议驱动程序指定的模式的网络帧上的唤醒事件的最低设备电源状态。

<a href="" id="minlinkchangewakeup"></a>**MinLinkChangeWakeUp**  
指定从其网络适配器可以发出信号的链接更改 （媒体连接或断开连接） 时唤醒事件的最低设备电源状态。

<a href="" id="supportedwakeupevents"></a>**SupportedWakeUpEvents**  
指定网络适配器支持的独立于媒体的唤醒事件。 这些事件不是特定于媒体类型。 例如，这些唤醒事件包括链接更改事件。

<a href="" id="mediaspecificwakeupevents"></a>**MediaSpecificWakeUpEvents**  
指定网络适配器支持的特定于媒体的唤醒事件。 例如，这些事件包括以下：

-   与访问点 (AP) 取消关联的 802.11 网络适配器。

-   移动宽带 (MB) 网络适配器检测到更改时向 MB 服务处于注册状态。

如果要卸载到低功耗状态中的网络适配器的协议的支持，它必须为协议支持相同的低功耗状态的微型端口驱动程序卸载它支持的模式匹配 WOL 事件;也就是说，在指定的值**MinPatternWakeUp**或**MinMagicPacketWakeUp**成员。

初始化 NDIS [ **NDIS\_PM\_功能**](https://msdn.microsoft.com/library/windows/hardware/ff566748)基础的网络适配器的当前可用的电源管理功能的结构并将其传递在绑定操作过程过量协议驱动程序协议。 NDIS 集**PowerManagementCapabilitiesEx**的成员[ **NDIS\_绑定\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff564832)结构，以指向 NDIS\_PM\_功能结构。

过量驱动程序可以使用[OID\_PM\_硬件\_功能](https://msdn.microsoft.com/library/windows/hardware/ff569767)OID 查询，以获取网络适配器的硬件电源管理功能。 NDIS 处理此 OID 请求代表微型端口驱动程序。 NDIS 微型端口驱动程序不支持所需 OID\_PM\_硬件\_功能 OID 请求。

过量驱动程序可以使用[OID\_PM\_当前\_功能](https://msdn.microsoft.com/library/windows/hardware/ff569765)OID 来查询网络适配器的当前可用的电源管理功能。 NDIS 处理此 OID 请求代表微型端口驱动程序。 NDIS 微型端口驱动程序不支持所需 OID\_PM\_当前\_功能 OID 请求。

 

 





