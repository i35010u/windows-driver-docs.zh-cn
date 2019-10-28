---
title: 停止关联后的操作
description: 停止关联后的操作
ms.assetid: 28400cad-1e77-4bcd-9b9a-103df5f06d10
keywords:
- 后关联操作 WDK 本机 802.11 IHV 扩展 DLL
- 停止关联后操作
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2dd8c0029a4654a4c351784346d040b93998986e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841819"
---
# <a name="stopping-a-post-association-operation"></a>停止关联后的操作




 

当发生以下情况之一时，操作系统将通过调用[*Dot11ExtIhvStopPostAssociate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_stop_post_associate) IHV 处理程序函数来终止关联后操作。

-   无线 LAN （WLAN）适配器使用 AP 完成解除对等操作。 在这种情况下，用于管理适配器的本机802.11 工作站使特定于媒体的[NDIS\_状态\_DOT11\_](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-dot11-disassociation)解除相关指示。 有关解除相关操作的详细信息，请参阅解除相关[操作](disassociation-operations.md)。

-   WLAN 适配器已禁用或删除。 在这种情况下，操作系统会在调用[*Dot11ExtIhvDeinitAdapter*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_deinit_adapter)函数之前调用[*Dot11ExtIhvStopPostAssociate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_stop_post_associate)函数。

操作系统将调用[*Dot11ExtIhvStopPostAssociate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_stop_post_associate)函数，以通知 IHV 扩展 DLL 为与 AP 关联而创建的数据端口已关闭。 操作系统调用此函数，而不考虑 DLL 是否已通过调用[**Dot11ExtPostAssociateCompletion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_post_associate_completion)完成后关联操作。

调用[*Dot11ExtIhvStopPostAssociate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_stop_post_associate)时，IHV 扩展必须释放为数据端口分配的所有资源。 如果未通过调用[**Dot11ExtPostAssociateCompletion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_post_associate_completion)完成后关联操作，则 IHV 扩展 DLL 必须在内部取消操作，但不得调用**Dot11ExtPostAssociateCompletion**。

 

 





