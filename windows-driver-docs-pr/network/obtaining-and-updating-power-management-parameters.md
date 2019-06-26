---
title: 获取和更新电源管理参数
description: 获取和更新电源管理参数
ms.assetid: 46c4d2ab-e6d9-4d23-bf40-0037b80b01af
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f9a209bcdfbe55d40169d79e8b9a7f78648a2589
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354530"
---
# <a name="obtaining-and-updating-power-management-parameters"></a>获取和更新电源管理参数





协议驱动程序可以使用[OID\_PM\_参数](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pm-parameters)OID 来查询当前已启用的网络适配器的硬件功能。 从查询中，成功返回后**InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)结构包含指向[ **NDIS\_PM\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_pm_parameters)结构。

协议驱动程序还可以使用 OID\_PM\_set 请求作为参数来启用或禁用网络适配器的当前硬件功能。 协议驱动程序提供一个指针到 NDIS\_PM\_结构中的参数**InformationBuffer** NDIS 成员\_OID\_请求结构。

**请注意**  协议驱动器不能禁用已启用的其他协议驱动程序的功能。 如果没有任何协议驱动程序启用一项功能，则不使用该功能。

 

**请注意**  NDIS 可幻数据包，低能耗上的断开连接的基于用户设置的功能和协议驱动程序不能禁用这些功能。

 

NDIS\_PM\_参数包括以下信息：

<a href="" id="enabledwolpacketpatterns"></a>**EnabledWoLPacketPatterns**  
包含对应于微型端口驱动程序中报告的功能标志**SupportedWoLPacketPatterns**的成员[ **NDIS\_PM\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_pm_capabilities)结构。 例如，启用的网络适配器以生成唤醒事件时接收通过 LAN (EAPOL) 请求标识符消息位图、 WOL 的幻数据包或 EAP。 可使用当前操作系统中的模式的完整列表，请参阅[ **NDIS\_PM\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_pm_parameters)参考页。

<a href="" id="enabledprotocoloffloads"></a>**EnabledProtocolOffloads**  
包含对应于微型端口驱动程序中报告的功能标志**SupportedProtocolOffloads**的成员[ **NDIS\_PM\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_pm_capabilities)结构。 NDIS 使用这些标志来启用或禁用网络适配器上的低能耗协议卸载功能。 例如，将卸载 IPv4 ARP、 IPv6 邻居招标 (NS)，或启用可靠安全的网络 (RSN) 4 路和 2 路握手的 IEEE 802.11 网络适配器。 在当前操作系统中支持协议卸载的完整列表，请参阅[ **NDIS\_PM\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_pm_parameters)参考页。

<a href="" id="wakeupflags"></a>**WakeUpFlags**  
包含 NDIS 使用来启用或禁用网络适配器上的唤醒功能的标志。

有关 NDIS 6.20，NDIS\_PM\_唤醒\_ON\_链接\_更改\_已启用标志可使唤醒 （媒体连接） 的链接更改的功能。 有关此标志的详细信息，请参阅[媒体断开连接的低开机](low-power-on-media-disconnect.md)。

从 NDIS 6.30，NDIS\_PM\_选择性\_挂起\_NDIS 选择性挂起基础 USB 网络适配器上已启用标志可以支持。 有关详细信息，请参阅[NDIS 选择性挂起](ndis-selective-suspend.md)。

当驱动程序集[OID\_PM\_参数](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pm-parameters)OID，NDIS 完成请求而无需将其转发到微型端口驱动程序。 NDIS 存储请求的设置，并将它们组合使用其他此类请求中的设置。

NDIS 转换到低功耗状态的网络适配器之前，NDIS 将 set 请求发送到包含从所有 NDIS 存储请求的组合的设置的微型端口驱动程序。 有关设置低功耗状态的详细信息，请参阅[低的电源可用于 LAN 唤醒](low-power-for-wake-on-lan.md)。

当前已启用的功能可以是硬件支持的功能子集。 有关硬件支持的功能的详细信息，请参阅[报告电源管理功能](reporting-power-management-capabilities.md)。

 

 





