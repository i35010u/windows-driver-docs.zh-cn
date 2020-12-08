---
title: 802.11 WLAN 适配器重置
description: 802.11 WLAN 适配器重置
keywords:
- 适配器 WDK 802.11 WLAN，重置
- WLAN 适配器 WDK，重置
- 正在重置 WLAN 适配器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b931227867810b9924d05a5c4c6c77953550f63e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96817685"
---
# <a name="80211-wlan-adapter-reset"></a>802.11 WLAN 适配器重置




 

每当需要将无线 LAN (WLAN) 适配器恢复到其初始化状态时，操作系统就会调用 [*Dot11ExtIhvAdapterReset*](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_adapter_reset) 。 当发生以下任一事件时，操作系统将调用此函数。

-   WLAN 适配器执行断开连接操作。 有关此操作的详细信息，请参阅 [断开连接操作](/previous-versions/windows/hardware/wireless/disconnection-operations)。

-   操作系统重置本机802.11 微型端口驱动程序，该驱动程序通过 [OID \_ DOT11 \_ RESET \_ 请求](/previous-versions/windows/hardware/wireless/oid-dot11-reset-request)的 set 请求来管理适配器。

调用 [*Dot11ExtIhvAdapterReset*](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_adapter_reset) 时，IHV 扩展 DLL 必须遵循这些准则。

-   IHV 扩展 DLL 必须将其状态还原到调用 [*Dot11ExtIhvInitAdapter*](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_init_adapter) 函数后所处的状态。 如果 DLL 配置了 WLAN 适配器上的专用设置，则必须将这些设置还原到调用 *Dot11ExtIhvInitAdapter* 后所处的相同状态。

-   如果 IHV 扩展 DLL 具有挂起的预关联操作（通过调用 [*Dot11ExtIhvPerformPreAssociate*](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_perform_pre_associate) IHV 处理程序函数启动），则 DLL 必须调用 [**Dot11ExtPreAssociateCompletion**](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_pre_associate_completion) 来取消操作。 在这种情况下，DLL 会将 **Dot11ExtPreAssociateCompletion** 的 *dwWin32Error* 参数设置为 "已 \_ 取消"。

    有关预关联操作的详细信息，请参阅 [预关联](pre-association-operations.md)操作。

-   如果 DLL 具有挂起的后关联操作（通过调用 [*Dot11ExtIhvPerformPostAssociate*](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_perform_post_associate) IHV 处理程序函数启动），则 dll 必须调用 [**Dot11ExtPostAssociateCompletion**](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_post_associate_completion) 来取消操作。 在这种情况下，DLL 会将 **Dot11ExtPostAssociateCompletion** 的 *dwWin32Error* 参数设置为 "已 \_ 取消"。

    有关后处理后操作的详细信息，请参阅 [之后的关联操作](post-association-operations.md)。

 

 
