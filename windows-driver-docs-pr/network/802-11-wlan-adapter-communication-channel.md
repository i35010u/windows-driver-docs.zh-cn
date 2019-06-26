---
title: 802.11 WLAN 适配器信道
description: 802.11 WLAN 适配器信道
ms.assetid: 6a4b07a5-3a0a-41cb-a5cf-74d44fb38192
keywords:
- 适配器 WDK 802.11 WLAN，通信通道
- WLAN 适配器 WDK，通信通道
- 通信通道 WDK 网络
- 传递通信通道 WDK 网络
- 数据包 WDK 网络，本机 802.11 IHV 扩展 DLL
- 指示 WDK 本机 802.11 IHV 扩展 DLL
- 发送操作 WDK 本机 802.11 IHV 扩展 DLL
- 接收操作 WDK 本机 802.11 IHV 扩展 DLL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c0f09c799b57bb809c47fa2b82b147a485ea28b0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379315"
---
# <a name="80211-wlan-adapter-communication-channel"></a>802.11 WLAN 适配器信道




 

操作系统提供 IHV 扩展 DLL 和本机 802.11 微型端口驱动程序之间传递通信通道。 IHV 扩展 DLL 访问以下操作的通信通道。

<a href="" id="--------sending-receiving-proprietary-configuration-data"></a> **发送/接收专有的配置数据**  
IHV 扩展 DLL NDIS 6.0 或更高版本的对象标识符 (OID) 方法将请求发送到本机 802.11 微型端口驱动程序通过调用[ **Dot11ExtNicSpecificExtension** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_nic_specific_extension)函数。 在内部，此函数发出的方法请求[OID\_DOT11\_NIC\_特定\_扩展](https://docs.microsoft.com/windows-hardware/drivers/network/oid-dot11-nic-specific-extension)微型端口驱动程序。 有关 NDIS OID 方法请求的详细信息，请参阅[ **NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)。

通常，IHV 扩展 DLL 调用**Dot11ExtNicSpecificExtension**来执行以下操作：

-   设置用于微型端口驱动程序或 WLAN 适配器的专有的配置参数。

-   查询专有的配置参数或从微型端口驱动程序或 WLAN 适配器的状态数据。

<a href="" id="receiving-notifications-indications"></a>**接收通知/指示**  
从本机 802.11 微型端口驱动程序通过调用以异步方式接收通知，IHV 扩展 DLL [ *Dot11ExtIhvReceiveIndication* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_receive_indication) IHV 处理程序函数。 操作系统将调用此函数，每当微型端口驱动程序，可以通过调用的特定于媒体的指示[ **NdisMIndicateStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismindicatestatusex)。 指示此类型的详细信息，请参阅[ **NDIS\_状态\_媒体\_特定\_指示**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-media-specific-indication)。

<a href="" id="sending-802-11-packets"></a>**发送 802.11 数据包**  
IHV 扩展 DLL 将 802.11 数据包发送到本机 802.11 微型端口驱动程序通过调用[ **Dot11ExtSendPacket** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_send_packet)函数。 微型端口驱动程序排队传输将 WLAN 适配器上的数据包。 当传输该数据包，操作系统将调用[ *Dot11ExtIhvSendPacketCompletion* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_send_packet_completion) IHV 处理程序函数。 有关发送数据包 IHV 扩展 DLL 的详细信息，请参阅[发送操作](send-operations.md)。

通常，IHV 扩展 DLL 调用[ **Dot11ExtSendPacket** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_send_packet)后关联操作期间发送安全数据包。 安全数据包基于支持的 DLL 和 WLAN 适配器上启用的身份验证算法。

<a href="" id="receiving-802-11-packets"></a>**接收 802.11 数据包**  
IHV 扩展 DLL 从本机 802.11 微型端口驱动程序通过调用接收 802.11 数据包[ *Dot11ExtIhvReceivePacket* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_receive_packet)函数。 操作系统将调用此函数为每个接收的数据包具有 EtherTypes 注册通过调用 DLL 的列表中的条目匹配 IEEE EtherType [ **Dot11ExtSetEtherTypeHandling** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_set_ethertype_handling). 有关接收数据包 IHV 扩展 dll 的详细信息，请参阅[接收操作](receive-operations.md)。

以下几点适用于 IHV 扩展 DLL 和本机 802.11 微型端口驱动程序之间的通信通道。

-   配置、 通知或指示通过此通道传输的数据的格式定义的独立硬件供应商 (IHV)，这是不透明的操作系统。

-   通过此通道接收的所有数据是序列化，数据由 IHV 扩展 DLL 或本机 802.11 微型端口驱动程序发送顺序传递。

 

 





