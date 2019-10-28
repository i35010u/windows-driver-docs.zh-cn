---
title: 802.11 WLAN 适配器移除
description: 802.11 WLAN 适配器移除
ms.assetid: 2181d284-7987-48db-b7a4-d1296d8313ed
keywords:
- 适配器 WDK 802.11 WLAN，删除
- WLAN 适配器 WDK，删除
- 删除 WLAN 适配器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 78c86c10a279c3bb662359ee5fec7823d23edebe
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838260"
---
# <a name="80211-wlan-adapter-removal"></a>802.11 WLAN 适配器移除




 

当删除或禁用无线 LAN （WLAN）适配器时，操作系统将调用[*Dot11ExtIhvDeinitAdapter*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_deinit_adapter)来通知 IHV 扩展 DLL 删除适配器。 操作系统还会在操作系统卸载 DLL 之前，为由 IHV 扩展 DLL 管理的每个适配器调用*Dot11ExtIhvDeinitAdapter*函数。

调用[*Dot11ExtIhvDeinitAdapter*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_deinit_adapter)时，IHV 扩展 DLL 必须遵循这些准则。

-   IHV 扩展 DLL 必须释放 WLAN 适配器的任何已分配资源。 特别是，通过调用[**Dot11ExtAllocateBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_allocate_buffer)分配的所有内存必须通过调用[**Dot11ExtFreeBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_free_buffer)释放。

-   调用[*Dot11ExtIhvDeinitAdapter*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_deinit_adapter)时，操作系统用于引用 WLAN 适配器的句柄不再有效。 调用[*Dot11ExtIhvInitAdapter*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_init_adapter)时，操作系统通过*hDot11SvcHandle*参数将其句柄传递到 IHV 扩展 DLL。

    在对*Dot11ExtIhvDeinitAdapter*函数的调用中，并在从调用返回后，DLL 不得在调用声明*hDot11SvcHandle*参数的任何 IHV 扩展性函数时使用句柄值，如[**Dot11ExtSendPacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_send_packet)。

-   如果 IHV 扩展 DLL 具有挂起的预关联操作（通过调用[*Dot11ExtIhvPerformPreAssociate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_perform_pre_associate) IHV 处理程序函数启动），则操作系统会通过调用[*将该操作视为已取消Dot11ExtIhvDeinitAdapter*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_deinit_adapter)函数。 在调用内，DLL 必须在内部取消预关联操作，但不能调用[**Dot11ExtPreAssociateCompletion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_pre_associate_completion)来完成预先关联的操作。

    有关预关联操作的详细信息，请参阅[预关联](pre-association-operations.md)操作。

-   如果 IHV 扩展 DLL 具有挂起的后关联操作（通过调用[*Dot11ExtIhvPerformPostAssociate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_perform_post_associate) IHV 处理程序函数启动），操作系统会通过调用[*Dot11ExtIhvStopPostAssociate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_stop_post_associate)函数，然后调用[*Dot11ExtIhvDeinitAdapter*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_deinit_adapter)。

    有关后处理后操作的详细信息，请参阅[之后的关联操作](post-association-operations.md)。

-   操作系统在操作系统卸载 DLL 之前，为由 IHV 扩展 DLL 管理的每个适配器调用[*Dot11ExtIhvDeinitAdapter*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_deinit_adapter)函数。 在这种情况下，在通过调用*Dot11ExtIhvDeinitAdapter*停止最后一个 WLAN 适配器后，操作系统将调用[*Dot11ExtIhvDeinitService*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_deinit_service) IHV 处理程序函数。

    有关此操作的详细信息，请参阅[DLL 停止操作](dll-stop-operations.md)。

 

 





