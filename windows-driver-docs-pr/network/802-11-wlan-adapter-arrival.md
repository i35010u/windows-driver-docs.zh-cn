---
title: 802.11 WLAN 适配器抵达
description: 802.11 WLAN 适配器抵达
ms.assetid: 4d533f32-0f98-4a65-ac1b-7a470e54ad29
keywords:
- 适配器 WDK 802.11 WLAN，抵达
- WLAN 适配器 WDK，抵达
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2f6b6e36b2079e365795f67e659df62df305d35e
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89215275"
---
# <a name="80211-wlan-adapter-arrival"></a>802.11 WLAN 适配器抵达




 

当操作系统检测到安装了 IHV 扩展 DLL (WLAN) 适配器的无线 LAN 时，操作系统将调用 [*Dot11ExtIhvInitAdapter*](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_init_adapter) IHV 处理程序函数。 只要 WLAN 适配器可用且已启用以供使用，操作系统就会调用此函数，例如插入 PCMCIA 适配器的时间。

调用 [*Dot11ExtIhvInitAdapter*](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_init_adapter) 函数时，将执行以下操作：

-   分配 WLAN 适配器上下文数据的数组，以及 WLAN 适配器所需的任何资源。

-   为 IHV 扩展 DLL 接收并使用的安全数据包注册 IEEE EtherTypes 的列表。

-   使用 IHV 定义的任何专有设置配置适配器。

调用 [*Dot11ExtIhvInitAdapter*](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_init_adapter) 时，必须遵循以下准则。

-   *HDot11SvcHandle*参数包含由操作系统为 WLAN 适配器分配的唯一句柄值。 IHV 扩展 DLL 必须保存此句柄值，并将其传递给与特定于适配器的处理（如[**Dot11ExtSetKeyMappingKey**](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_set_key_mapping_key)）相关的 IHV 扩展性函数的*hDot11SvcHandle*参数。

    通常，DLL 会在其 WLAN 适配器上下文数组的成员内保存此句柄值。

-   IHV 扩展 DLL 必须通过 *phIhvExtAdapter* 参数为 WLAN 适配器返回唯一的句柄值。 操作系统将句柄值传递到与特定于适配器的处理相关的 IHV 处理程序函数（如[*Dot11ExtIhvReceiveIndication*](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_receive_indication)）的*hIhvExtAdapter*参数。

    通常，DLL 返回作为句柄值的 WLAN 适配器上下文数组的地址。

-   IHV 扩展 DLL 会调用 [**Dot11ExtSetEtherTypeHandling**](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_set_ethertype_handling) ，以便为 DLL 将接收的安全数据包注册 IEEE EtherTypes 列表。 IHV 扩展 DLL 还可以指定将从负载解密中排除的 EtherTypes 的列表。 有关注册 EtherTypes 的详细信息，请参阅 [IEEE EtherType 处理](ieee-ethertype-handling.md)。

    注册 EtherTypes 后，操作系统将为其 EtherType 与列表中的条目相匹配的每个数据包调用 [*Dot11ExtIhvReceivePacket*](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_receive_packet) IHV 处理程序函数。

-   操作系统通过 (Oid) 的本机802.11 对象标识符的 set 请求来配置具有标准802.11 参数的适配器。 有关这些 Oid 的详细信息，请参阅 [本机802.11 无线 LAN oid](/previous-versions/windows/hardware/wireless/native-802-11-oids)。

    但是，DLL 可以通过调用 [**Dot11ExtNicSpecificExtension**](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_nic_specific_extension) 函数，使用专用参数配置适配器。 通过此函数调用，DLL 可直接与本机802.11 微型端口驱动程序通信，该驱动程序管理 WLAN 适配器和发出查询，或基于由 IHV 定义的专有格式将请求设置为驱动程序。

    有关 DLL 和 WLAN 适配器进行通信的接口的详细信息，请参阅 [802.11 WLAN 适配器通信通道](802-11-wlan-adapter-communication-channel.md)。

 

 