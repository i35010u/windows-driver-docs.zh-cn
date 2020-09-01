---
title: 802.11 WLAN 适配器信道
description: 802.11 WLAN 适配器信道
ms.assetid: 6a4b07a5-3a0a-41cb-a5cf-74d44fb38192
keywords:
- 适配器 WDK 802.11 WLAN，通信通道
- WLAN 适配器 WDK，通信通道
- 通信通道 WDK 网络
- 传递通信通道 WDK 网络
- 包 WDK 网络，本机 802.11 IHV 扩展 DLL
- 指示 WDK 本机 802.11 IHV 扩展 DLL
- 发送操作 WDK Native 802.11 IHV 扩展 DLL
- 接收操作 WDK 本机 802.11 IHV 扩展 DLL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bbc00c9acaf2cad00ef52606b7d5cffc61d23d52
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89212553"
---
# <a name="80211-wlan-adapter-communication-channel"></a>802.11 WLAN 适配器信道




 

操作系统在 IHV 扩展 DLL 和本机802.11 微型端口驱动程序之间提供传递通信通道。 IHV 扩展 DLL 访问以下操作的通信通道。

<a href="" id="--------sending-receiving-proprietary-configuration-data"></a>**发送/接收专用配置数据**  
IHV 扩展 DLL 通过调用 [**Dot11ExtNicSpecificExtension**](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_nic_specific_extension) 函数将 NDIS 6.0 或更高版本的对象标识符 () OID 发送到本机802.11 微型端口驱动程序。 在内部，此函数将向微型端口驱动程序发出 [OID \_ DOT11 \_ NIC \_ 特定 \_ 扩展](/previous-versions/windows/hardware/wireless/oid-dot11-nic-specific-extension) 的方法请求。 有关 NDIS OID 方法请求的详细信息，请参阅 [**ndis \_ oid \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)。

通常，IHV 扩展 DLL 调用 **Dot11ExtNicSpecificExtension** 来执行以下操作：

-   为微型端口驱动程序或 WLAN 适配器设置专用配置参数。

-   从微型端口驱动程序或 WLAN 适配器查询专有的配置参数或状态数据。

<a href="" id="receiving-notifications-indications"></a>**正在接收通知/指示**  
IHV 扩展 DLL 通过调用 [*Dot11ExtIhvReceiveIndication*](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_receive_indication) IHV 处理程序函数，从本机802.11 微型端口驱动程序异步接收通知。 每当微型端口驱动程序通过调用 [**NdisMIndicateStatusEx**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatestatusex)进行特定于媒体的指示时，操作系统就会调用此函数。 有关此类指示的详细信息，请参阅 [**NDIS \_ 状态 \_ 媒体 \_ 特定 \_ 指示**](./ndis-status-media-specific-indication.md)。

<a href="" id="sending-802-11-packets"></a>**发送802.11 数据包**  
IHV 扩展 DLL 通过调用 [**Dot11ExtSendPacket**](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_send_packet) 函数将802.11 数据包发送到本机802.11 微型端口驱动程序。 微型端口驱动程序将 WLAN 适配器上的数据包排队以进行传输。 传输数据包后，操作系统将调用 [*Dot11ExtIhvSendPacketCompletion*](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_send_packet_completion) IHV 处理程序函数。 有关通过 IHV 扩展 DLL 发送数据包的详细信息，请参阅 [发送操作](send-operations.md)。

通常情况下，IHV 扩展 DLL 会调用 [**Dot11ExtSendPacket**](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_send_packet) ，以便在之后的关联操作期间发送安全数据包。 安全数据包基于 DLL 支持的身份验证算法，并在 WLAN 适配器上启用。

<a href="" id="receiving-802-11-packets"></a>**接收802.11 数据包**  
IHV 扩展 DLL 通过对 [*Dot11ExtIhvReceivePacket*](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_receive_packet) 函数的调用从本机802.11 微型端口驱动程序接收802.11 数据包。 操作系统为每个已接收的数据包调用此函数，该函数具有与通过调用 [**Dot11ExtSetEtherTypeHandling**](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_set_ethertype_handling)调用的 EtherTypes 列表中的条目相匹配的 EtherType。 有关通过 IHV 扩展 DLL 接收数据包的详细信息，请参阅 [接收操作](receive-operations.md)。

以下几点适用于 IHV 扩展 DLL 和本机802.11 微型端口驱动程序之间的信道。

-   通过此通道传输的配置、通知或指示数据具有由独立硬件供应商定义的格式 (IHV) ，这对操作系统不透明。

-   通过此通道接收的所有数据都将按 IHV 扩展 DLL 或本机802.11 微型端口驱动程序发送数据的顺序进行序列化和传递。

 

 