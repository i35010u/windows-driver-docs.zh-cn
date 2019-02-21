---
title: 802.11 WLAN 适配器通信通道
description: 802.11 WLAN 适配器通信通道
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
ms.openlocfilehash: 6b97fcba7663f46a53304ad506375428e7195ac8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522534"
---
# <a name="80211-wlan-adapter-communication-channel"></a>802.11 WLAN 适配器通信通道




 

操作系统提供 IHV 扩展 DLL 和本机 802.11 微型端口驱动程序之间传递通信通道。 IHV 扩展 DLL 访问以下操作的通信通道。

<a href="" id="--------sending-receiving-proprietary-configuration-data"></a> **发送/接收专有的配置数据**  
IHV 扩展 DLL NDIS 6.0 或更高版本的对象标识符 (OID) 方法将请求发送到本机 802.11 微型端口驱动程序通过调用[ **Dot11ExtNicSpecificExtension** ](https://msdn.microsoft.com/library/windows/hardware/ff547526)函数。 在内部，此函数发出的方法请求[OID\_DOT11\_NIC\_特定\_扩展](https://msdn.microsoft.com/library/windows/hardware/ff569393)微型端口驱动程序。 有关 NDIS OID 方法请求的详细信息，请参阅[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)。

通常，IHV 扩展 DLL 调用**Dot11ExtNicSpecificExtension**来执行以下操作：

-   设置用于微型端口驱动程序或 WLAN 适配器的专有的配置参数。

-   查询专有的配置参数或从微型端口驱动程序或 WLAN 适配器的状态数据。

<a href="" id="receiving-notifications-indications"></a>**接收通知/指示**  
从本机 802.11 微型端口驱动程序通过调用以异步方式接收通知，IHV 扩展 DLL [ *Dot11ExtIhvReceiveIndication* ](https://msdn.microsoft.com/library/windows/hardware/ff547512) IHV 处理程序函数。 操作系统将调用此函数，每当微型端口驱动程序，可以通过调用的特定于媒体的指示[ **NdisMIndicateStatusEx**](https://msdn.microsoft.com/library/windows/hardware/ff563600)。 指示此类型的详细信息，请参阅[ **NDIS\_状态\_媒体\_特定\_指示**](https://msdn.microsoft.com/library/windows/hardware/ff567399)。

<a href="" id="sending-802-11-packets"></a>**发送 802.11 数据包**  
IHV 扩展 DLL 将 802.11 数据包发送到本机 802.11 微型端口驱动程序通过调用[ **Dot11ExtSendPacket** ](https://msdn.microsoft.com/library/windows/hardware/ff547563)函数。 微型端口驱动程序排队传输将 WLAN 适配器上的数据包。 当传输该数据包，操作系统将调用[ *Dot11ExtIhvSendPacketCompletion* ](https://msdn.microsoft.com/library/windows/hardware/ff547516) IHV 处理程序函数。 有关发送数据包 IHV 扩展 DLL 的详细信息，请参阅[发送操作](send-operations.md)。

通常，IHV 扩展 DLL 调用[ **Dot11ExtSendPacket** ](https://msdn.microsoft.com/library/windows/hardware/ff547563)后关联操作期间发送安全数据包。 安全数据包基于支持的 DLL 和 WLAN 适配器上启用的身份验证算法。

<a href="" id="receiving-802-11-packets"></a>**接收 802.11 数据包**  
IHV 扩展 DLL 从本机 802.11 微型端口驱动程序通过调用接收 802.11 数据包[ *Dot11ExtIhvReceivePacket* ](https://msdn.microsoft.com/library/windows/hardware/ff547513)函数。 操作系统将调用此函数为每个接收的数据包具有 EtherTypes 注册通过调用 DLL 的列表中的条目匹配 IEEE EtherType [ **Dot11ExtSetEtherTypeHandling** ](https://msdn.microsoft.com/library/windows/hardware/ff547587). 有关接收数据包 IHV 扩展 dll 的详细信息，请参阅[接收操作](receive-operations.md)。

以下几点适用于 IHV 扩展 DLL 和本机 802.11 微型端口驱动程序之间的通信通道。

-   配置、 通知或指示通过此通道传输的数据的格式定义的独立硬件供应商 (IHV)，这是不透明的操作系统。

-   通过此通道接收的所有数据是序列化，数据由 IHV 扩展 DLL 或本机 802.11 微型端口驱动程序发送顺序传递。

 

 





