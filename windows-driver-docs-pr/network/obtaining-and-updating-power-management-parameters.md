---
title: 获取和更新电源管理参数
description: 获取和更新电源管理参数
ms.assetid: 46c4d2ab-e6d9-4d23-bf40-0037b80b01af
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0cc66e3a16e2e9fef68af78bd1bd8c6d6442b3f5
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89215498"
---
# <a name="obtaining-and-updating-power-management-parameters"></a>获取和更新电源管理参数





协议驱动程序可以使用 [oid \_ PM \_ 参数](./oid-pm-parameters.md) OID 来查询当前启用的网络适配器的硬件功能。 成功从查询返回后， [**ndis \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含指向[**NDIS \_ PM \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_parameters)结构的指针。

协议驱动程序还可以将 OID \_ PM \_ 参数用作集请求，以启用或禁用网络适配器的当前硬件功能。 协议驱动程序在 \_ \_ ndis **InformationBuffer** \_ OID 请求结构的 InformationBuffer 成员中提供了一个指向 ndis PM 参数结构的指针 \_ 。

**注意**   协议驱动器无法禁用由其他协议驱动程序启用的功能。 如果没有任何协议驱动程序启用功能，则不会使用该功能。

 

**注意**   NDIS 基于用户设置启用幻数据包和低功耗断开功能，并且这些功能不能由协议驱动程序禁用。

 

NDIS \_ PM \_ 参数包含以下信息：

<a href="" id="enabledwolpacketpatterns"></a>**EnabledWoLPacketPatterns**  
包含对应于小型端口驱动程序在[**NDIS \_ PM \_ 功能**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_capabilities)结构的**SupportedWoLPacketPatterns**成员中报告的功能的标志。 例如，当网络适配器接收到位图、WOL 幻数据包或通过 LAN 的 EAP (EAPOL) 请求标识符消息时，该适配器将生成唤醒事件。 有关当前操作系统中可能存在的模式的完整列表，请参阅 " [**NDIS \_ PM \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_parameters) 参考" 页。

<a href="" id="enabledprotocoloffloads"></a>**EnabledProtocolOffloads**  
包含对应于小型端口驱动程序在[**NDIS \_ PM \_ 功能**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_capabilities)结构的**SupportedProtocolOffloads**成员中报告的功能的标志。 NDIS 使用这些标志在网络适配器上启用或禁用低功率协议卸载功能。 例如，IPv4 ARP 的网络适配器卸载、IPv6 邻居请求 (NS) 或 IEEE 802.11 稳健安全网络 (RSN) 4 向和双向握手处于启用状态。 有关当前操作系统中支持的协议卸载的完整列表，请参阅 " [**NDIS \_ PM \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_parameters) 参考" 页。

<a href="" id="wakeupflags"></a>**WakeUpFlags**  
包含 NDIS 用于启用或禁用网络适配器上的唤醒功能的标志。

对于 NDIS 6.20，启用 "NDIS \_ PM \_ 唤醒" 链接 " \_ \_ \_ \_ 已启用" 标志使你能够在更改 (media connect) 的链接时唤醒。 有关此标志的详细信息，请参阅 [低能耗媒体断开连接](low-power-on-media-disconnect.md)。

从 NDIS 6.30 开始，NDIS \_ PM \_ 选择性 \_ 挂起 \_ 已启用标志支持在基础 USB 网络适配器上支持 NDIS 选择性挂起。 有关详细信息，请参阅 " [NDIS 选择性挂起](ndis-selective-suspend.md)"。

当驱动程序设置 [oid \_ PM \_ 参数](./oid-pm-parameters.md) oid 时，NDIS 完成请求，而不将其转发给微型端口驱动程序。 NDIS 存储请求的设置，并将它们与其他此类请求中的设置组合在一起。

在 NDIS 将网络适配器转换为低功率状态之前，NDIS 会将 set 请求发送到包含 NDIS 存储的所有请求中的组合设置的微型端口驱动程序。 有关设置低功耗状态的详细信息，请参阅 [LAN 唤醒的低功率](low-power-for-wake-on-lan.md)。

当前启用的功能可以是硬件支持的功能的子集。 有关硬件支持的功能的详细信息，请参阅 [报告电源管理功能](reporting-power-management-capabilities.md)。

 

