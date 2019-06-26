---
title: 802.11 WLAN 适配器重置
description: 802.11 WLAN 适配器重置
ms.assetid: 1f993977-b4a1-42ec-8de3-2f4855db93a7
keywords:
- WDK 802.11 WLAN 适配器重置
- WLAN 适配器 WDK，重置
- 重置 WLAN 适配器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cb5e4871fd94b36c4ecd83fc79d04fd66a7ba4b7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379306"
---
# <a name="80211-wlan-adapter-reset"></a>802.11 WLAN 适配器重置




 

操作系统调用[ *Dot11ExtIhvAdapterReset* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_adapter_reset)只要有必要还原到其已初始化状态的无线 LAN (WLAN) 适配器。 出现以下事件之一时，操作系统将调用此函数。

-   将 WLAN 适配器执行断开连接操作。 有关此操作的详细信息，请参阅[断开连接操作](disconnection-operations.md)。

-   操作系统将本机 802.11 微型端口驱动程序，它管理的适配器，通过设置请求的重置[OID\_DOT11\_重置\_请求](https://docs.microsoft.com/windows-hardware/drivers/network/oid-dot11-reset-request)。

当[ *Dot11ExtIhvAdapterReset* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_adapter_reset)是调用，IHV 扩展 DLL 必须遵循这些准则。

-   IHV 扩展 DLL 必须将其状态还原到相同的状态后处于[ *Dot11ExtIhvInitAdapter* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_init_adapter)调用函数。 DLL 将 WLAN 适配器上配置专用设置，则其必须还原到它们后所处的相同状态的这些设置*Dot11ExtIhvInitAdapter*调用。

-   如果 IHV 扩展 DLL 具有一个挂起的预关联操作，这通过调用启动[ *Dot11ExtIhvPerformPreAssociate* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_perform_pre_associate) IHV 处理程序函数，必须调用 DLL [**Dot11ExtPreAssociateCompletion** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_pre_associate_completion)取消该操作。 在此情况下，设置 DLL *dwWin32Error*的参数**Dot11ExtPreAssociateCompletion**错误\_已取消。

    有关预关联操作的详细信息，请参阅[预关联操作](pre-association-operations.md)。

-   如果 DLL 具有挂起的后期关联操作，通过调用已启动[ *Dot11ExtIhvPerformPostAssociate* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_perform_post_associate) IHV 处理程序函数，必须调用 DLL [ **Dot11ExtPostAssociateCompletion** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_post_associate_completion)取消该操作。 在此情况下，设置 DLL *dwWin32Error*的参数**Dot11ExtPostAssociateCompletion**错误\_已取消。

    有关后关联操作的详细信息，请参阅[后期关联操作](post-association-operations.md)。

 

 





