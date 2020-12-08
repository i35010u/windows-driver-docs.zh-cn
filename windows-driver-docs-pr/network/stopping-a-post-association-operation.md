---
title: 停止关联后的操作
description: 停止关联后的操作
keywords:
- 后关联操作 WDK 本机 802.11 IHV 扩展 DLL
- 停止关联后操作
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f274dab7e468186b7a89f618f2400cc37c2f3e4b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96790419"
---
# <a name="stopping-a-post-association-operation"></a>停止关联后的操作




 

当发生以下情况之一时，操作系统将通过调用 [*Dot11ExtIhvStopPostAssociate*](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_stop_post_associate) IHV 处理程序函数来终止关联后操作。

-   无线 LAN (WLAN) 适配器完成与 AP 的解除解除操作。 在这种情况下，用于管理适配器的本机802.11 工作站使特定于媒体的 [NDIS \_ 状态 \_ DOT11 \_ ](/previous-versions/windows/hardware/wireless/ndis-status-dot11-disassociation) 解除相关指示。 有关解除相关操作的详细信息，请参阅解除相关 [操作](/previous-versions/windows/hardware/wireless/disassociation-operations)。

-   WLAN 适配器已禁用或删除。 在这种情况下，操作系统会在调用 [*Dot11ExtIhvDeinitAdapter*](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_deinit_adapter)函数之前调用 [*Dot11ExtIhvStopPostAssociate*](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_stop_post_associate)函数。

操作系统将调用 [*Dot11ExtIhvStopPostAssociate*](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_stop_post_associate) 函数，以通知 IHV 扩展 DLL 为与 AP 关联而创建的数据端口已关闭。 操作系统调用此函数，而不考虑 DLL 是否已通过调用 [**Dot11ExtPostAssociateCompletion**](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_post_associate_completion)完成后关联操作。

调用 [*Dot11ExtIhvStopPostAssociate*](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_stop_post_associate) 时，IHV 扩展必须释放为数据端口分配的所有资源。 如果未通过调用 [**Dot11ExtPostAssociateCompletion**](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_post_associate_completion)完成后关联操作，则 IHV 扩展 DLL 必须在内部取消操作，但不得调用 **Dot11ExtPostAssociateCompletion**。

 

 
