---
title: IEEE EtherType 处理
description: IEEE EtherType 处理
ms.assetid: ddd7244b-05a0-4ee8-b9aa-300015fbe3bd
keywords:
- 发送操作 WDK 本机 802.11 IHV 扩展 DLL
- 接收操作 WDK 本机 802.11 IHV 扩展 DLL
- IEEE EtherType 处理 WDK 本机 802.11 IHV 扩展 DLL
- EtherType 处理 WDK 本机 802.11 IHV 扩展 DLL
- 隐私异常 WDK 本机 802.11 IHV 扩展 DLL
- 解密 WDK 本机 802.11 IHV 扩展 DLL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4b9e333c590e078f68b84c3733124b00aa18893f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384554"
---
# <a name="ieee-ethertype-handling"></a>IEEE EtherType 处理




 

IHV 扩展 DLL 可以指定以进行特殊处理的无线 LAN (WLAN) 适配器接收的数据包的 IEEE EtherTypes 列表。 可以指定以下类型的以太网类型处理。

<a href="" id="privacy-exemptions"></a>**隐私例外**  
IHV 扩展 DLL 可以指定收到的数据包的数据包解密例外。 例如，该 DLL 可以指定允许使用指定 EtherType 数据包被接收未加密，即使 WLAN 适配器上配置了匹配密码密钥。

<a href="" id="ethertype-registration"></a>**以太网类型注册**  
IHV 扩展 DLL 可以注册 EtherTypes，它会处理和使用。 操作系统将转发数据包匹配到通过调用 DLL 注册的 EtherType [ *Dot11ExtIhvReceivePacket* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_receive_packet)函数。

IHV 扩展 DLL 指定处理通过调用 EtherType [ **Dot11ExtSetEtherTypeHandling** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_set_ethertype_handling)函数。 调用此函数时，IHV 扩展 DLL 必须遵循这些准则。

-   只能调用 IHV 扩展 DLL [ **Dot11ExtSetEtherTypeHandling** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_set_ethertype_handling)在完成预关联操作之前的任何时间。 有关此操作的详细信息，请参阅[预关联操作](pre-association-operations.md)。

-   IHV 扩展 DLL 指定其列表访问一系列的零个或更多的隐私例外[ **DOT11\_隐私\_免除**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/windot11/ns-windot11-dot11_privacy_exemption)结构。 如果 IHV 扩展 DLL 不会调用[ **Dot11ExtSetEtherTypeHandling**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_set_ethertype_handling)，操作系统将默认为空列表的任何 802.11 的关联的访问点 (AP) 的隐私例外。
    **请注意**  For Windows Vista 中，只有在基础结构的基本服务设置 (BSS) 网络 IHV 扩展 DLL 支持。

     

-   IHV 扩展 DLL 注册将收到的零个或多个 EtherTypes 的列表。 通常情况下，该 DLL 注册为在后期关联操作过程中处理安全数据包 EtherTypes。 有关此操作的详细信息，请参阅[后期关联操作](post-association-operations.md)。

    如果 IHV 扩展 DLL 不会调用[ **Dot11ExtSetEtherTypeHandling**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_set_ethertype_handling)，操作系统将默认为已注册 EtherTypes AP 使用任何 802.11 关联一个空列表。

-   IHV 扩展 DLL 将通过调用完成预关联操作后[ **Dot11ExtPreAssociateCompletion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_pre_associate_completion)，隐私例外和 EtherType 注册通过指定的列表调用到[ **Dot11ExtSetEtherTypeHandling** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_set_ethertype_handling)应用于每个 802.11 的关联所做的 WLAN 适配器连接到基本服务集 (BSS) 网络时。

-   操作系统调用之前清除的隐私例外和 EtherType 注册列表[ *Dot11ExtIhvAdapterReset*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_adapter_reset)。

 

 





