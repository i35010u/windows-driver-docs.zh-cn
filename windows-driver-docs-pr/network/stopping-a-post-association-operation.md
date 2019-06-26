---
title: 停止关联后的操作
description: 停止关联后的操作
ms.assetid: 28400cad-1e77-4bcd-9b9a-103df5f06d10
keywords:
- 后关联操作 WDK 本机 802.11 IHV 扩展 DLL
- 停止后关联操作
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7094c852c31a918cca6bf6c1152b2a4a51022bad
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383584"
---
# <a name="stopping-a-post-association-operation"></a>停止关联后的操作




 

操作系统通过调用来终止后关联操作[ *Dot11ExtIhvStopPostAssociate* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_stop_post_associate) IHV 处理程序函数每次发生下列情况之一时。

-   无线 LAN (WLAN) 适配器完成同 ap 的解除关联操作。 在此情况下，本机 802.11 工作站，用于管理该适配器，使媒体特定[NDIS\_状态\_DOT11\_解除关联](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-dot11-disassociation)指示。 有关解除关联操作的详细信息，请参阅[解除关联操作](disassociation-operations.md)。

-   将 WLAN 适配器是禁用或删除。 在此情况下，操作系统将调用[ *Dot11ExtIhvStopPostAssociate* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_stop_post_associate)函数调用之前[ *Dot11ExtIhvDeinitAdapter*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_deinit_adapter)函数。

操作系统调用[ *Dot11ExtIhvStopPostAssociate* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_stop_post_associate)函数，以通知创建为与亚太的关联的数据端口已关闭 IHV 扩展 DLL。 操作系统将调用此函数而不考虑该 DLL 是否已完成后关联操作通过调用[ **Dot11ExtPostAssociateCompletion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_post_associate_completion)。

当[ *Dot11ExtIhvStopPostAssociate* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_stop_post_associate)是调用，IHV 扩展必须释放所有的数据端口分配的资源。 如果后期关联操作未完成通过调用[ **Dot11ExtPostAssociateCompletion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_post_associate_completion)，IHV 扩展 DLL 必须在内部取消操作，但不能调用**Dot11ExtPostAssociateCompletion**。

 

 





