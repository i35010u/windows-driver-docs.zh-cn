---
title: IEEE EtherType 处理
description: IEEE EtherType 处理
ms.assetid: ddd7244b-05a0-4ee8-b9aa-300015fbe3bd
keywords:
- 发送操作 WDK Native 802.11 IHV 扩展 DLL
- 接收操作 WDK 本机 802.11 IHV 扩展 DLL
- IEEE EtherType 处理 WDK Native 802.11 IHV 扩展 DLL
- EtherType 处理 WDK Native 802.11 IHV 扩展 DLL
- 隐私异常 WDK 本机 802.11 IHV 扩展 DLL
- 解密 WDK 本机 802.11 IHV 扩展 DLL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9c6da1de936ce6e6b25235b451fa2b001c5538a9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72823813"
---
# <a name="ieee-ethertype-handling"></a>IEEE EtherType 处理




 

IHV 扩展 DLL 可以指定 IEEE EtherTypes 的列表，用于特殊处理无线 LAN （WLAN）适配器接收的数据包。 可以指定以下类型的 EtherType 处理。

<a href="" id="privacy-exemptions"></a>**隐私例外**  
IHV 扩展 DLL 可以为接收的数据包指定数据包解密例外。 例如，如果在 WLAN 适配器上配置了匹配的密码密钥，则 DLL 可以指定允许以未加密的形式接收具有指定 EtherType 的数据包。

<a href="" id="ethertype-registration"></a>**EtherType 注册**  
IHV 扩展 DLL 可以注册它将处理和使用的 EtherTypes。 操作系统通过调用[*Dot11ExtIhvReceivePacket*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_receive_packet)函数将与已注册的 EtherType 匹配的数据包转发到 DLL。

IHV 扩展 DLL 通过调用[**Dot11ExtSetEtherTypeHandling**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_set_ethertype_handling)函数指定 EtherType 处理。 调用此函数时，IHV 扩展 DLL 必须遵循这些准则。

-   在完成预关联操作之前，IHV 扩展 DLL 只能调用[**Dot11ExtSetEtherTypeHandling**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_set_ethertype_handling) 。 有关此操作的详细信息，请参阅[预关联操作](pre-association-operations.md)。

-   IHV 扩展 DLL 通过零个或多个[**DOT11\_隐私\_免除**](https://docs.microsoft.com/windows-hardware/drivers/ddi/windot11/ns-windot11-dot11_privacy_exemption)结构的数组指定其隐私免除列表。 如果 IHV 扩展 DLL 未调用[**Dot11ExtSetEtherTypeHandling**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_set_ethertype_handling)，则操作系统将默认为任何与访问点（AP）存在802.11 关联的隐私例外列表。
    **注意**  对于 Windows VISTA，IHV 扩展 DLL 仅支持基础结构基本服务集（BSS）网络。

     

-   IHV 扩展 DLL 注册一个列表，其中列出了它将接收的零个或多个 EtherTypes。 通常，DLL 会在后期关联操作过程中为它处理的安全数据包注册 EtherTypes。 有关此操作的详细信息，请参阅[关联后操作](post-association-operations.md)。

    如果 IHV 扩展 DLL 未调用[**Dot11ExtSetEtherTypeHandling**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_set_ethertype_handling)，则操作系统将默认为任何802.11 与 AP 关联的已注册 EtherTypes 的空列表。

-   在 IHV 扩展 DLL 通过调用[**Dot11ExtPreAssociateCompletion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_pre_associate_completion)完成了预关联操作后，通过对[**Dot11ExtSetEtherTypeHandling**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_set_ethertype_handling)的调用指定的隐私免除和 EtherType 注册的列表是已应用于 WLAN 适配器在连接到基本服务集（BSS）网络时所建立的每个802.11 关联。

-   在调用[*Dot11ExtIhvAdapterReset*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_adapter_reset)之前，操作系统会清除隐私例外和 EtherType 注册列表。

 

 





