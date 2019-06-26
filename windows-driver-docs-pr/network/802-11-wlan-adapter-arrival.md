---
title: 802.11 WLAN 适配器抵达
description: 802.11 WLAN 适配器抵达
ms.assetid: 4d533f32-0f98-4a65-ac1b-7a470e54ad29
keywords:
- 适配器 WDK 802.11 WLAN，到达的请求
- WLAN 适配器 WDK，到达的请求
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e7bb676d2760550647c7d3e966cc851ba0c00ef8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379314"
---
# <a name="80211-wlan-adapter-arrival"></a>802.11 WLAN 适配器抵达




 

当操作系统检测到为其安装 IHV 扩展 DLL 的无线 LAN (WLAN) 适配器时，操作系统将调用[ *Dot11ExtIhvInitAdapter* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_init_adapter) IHV 处理程序函数。 操作系统将调用此函数时 WLAN 适配器成为可用且已启用供使用，例如当插入 PCMCIA 适配器。

当[ *Dot11ExtIhvInitAdapter* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_init_adapter)调用函数，IHV 扩展 DLL 执行以下操作：

-   WLAN 适配器的上下文数据以及 DLL 将 WLAN 适配器所需的任何资源分配一个数组。

-   注册为安全数据包接收并由 IHV 扩展 DLL 的 IEEE EtherTypes 列表。

-   使用由 IHV 定义任何专有设置来配置适配器。

IHV 扩展 DLL 必须遵循这些准则时[ *Dot11ExtIhvInitAdapter* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_init_adapter)调用。

-   *HDot11SvcHandle*参数包含将 WLAN 适配器操作系统分配一个唯一的句柄值。 IHV 扩展 DLL 必须保存此句柄值并将其传递给*hDot11SvcHandle* IHV 扩展性函数的参数与特定于适配器的处理，如相关[ **Dot11ExtSetKeyMappingKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_set_key_mapping_key)。

    通常情况下，DLL 将保存其 WLAN 适配器上下文数组的一个成员中此句柄值。

-   IHV 扩展 DLL 必须唯一的句柄为返回值通过将 WLAN 适配器*phIhvExtAdapter*参数。 操作系统句柄将值传递给*hIhvExtAdapter* IHV 处理程序函数的参数与特定于适配器的处理，如相关[ *Dot11ExtIhvReceiveIndication*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_receive_indication).

    通常情况下，该 DLL 的句柄值作为返回 WLAN 适配器上下文数组的地址。

-   IHV 扩展 DLL 调用[ **Dot11ExtSetEtherTypeHandling** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_set_ethertype_handling)注册的 DLL 将接收的安全数据包 IEEE EtherTypes 列表。 IHV 扩展 DLL 还可以指定将从有效负载解密中排除的 EtherTypes 的列表。 有关注册 EtherTypes 的详细信息，请参阅[IEEE EtherType 处理](ieee-ethertype-handling.md)。

    EtherTypes 注册后，操作系统将调用[ *Dot11ExtIhvReceivePacket* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_receive_packet)其 EtherType 与列表中的某个条目匹配的每个数据包的 IHV 处理程序函数。

-   操作系统通过本机 802.11 对象标识符 (Oid) 的集请求的标准 802.11 参数与配置的适配器。 有关这些 Oid 的详细信息，请参阅[本机 802.11 无线 LAN Oid](https://docs.microsoft.com/windows-hardware/drivers/network/native-802-11-oids)。

    但是，该 DLL 可以配置适配器使用专有参数通过调用[ **Dot11ExtNicSpecificExtension** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_nic_specific_extension)函数。 通过此函数调用，该 DLL 可以直接与管理 WLAN 适配器和问题查询的本机 802.11 微型端口驱动程序进行通信或将请求设置为基于定义 IHV 的专有格式的驱动程序。

    有关通过该 DLL 和 WLAN 适配器进行通信的接口的详细信息，请参阅[802.11 WLAN 适配器通信通道](802-11-wlan-adapter-communication-channel.md)。

 

 





