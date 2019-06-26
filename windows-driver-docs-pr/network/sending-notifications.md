---
title: 发送通知
description: 发送通知
ms.assetid: 55e0f41c-e042-4170-bedd-160b6c457365
keywords:
- 通知 WDK 本机 802.11 IHV 扩展 DLL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bfc21e7ac954406c4c7fd470ab5933ac3f2bc1da
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386838"
---
# <a name="sending-notifications"></a>发送通知




 

IHV 扩展 DLL 调用[ **Dot11ExtSendNotification** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_send_notification)函数将通知发送到任何服务或应用程序已注册的通知。 若要接收通知，服务或应用程序必须注册使用自动配置管理器 (ACM) 通过调用**WlanRegisterNotification**函数。 有关此函数的详细信息，请参阅 Microsoft Windows SDK 文档。

**请注意**  服务或应用程序必须使用注册通知的源值的 L2\_通知\_源\_WLAN\_IHV 才能通过接收通知调用[ **Dot11ExtSendNotification** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_send_notification)函数。

 

调用时[ **Dot11ExtSendNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_send_notification)，IHV 扩展 DLL 将传递一个指向[ **L2\_通知\_数据**](https://docs.microsoft.com/windows/desktop/api/l2cmn/ns-l2cmn-_l2_notification_data)结构*pNotificationData*参数。 L2\_通知\_数据定义通知的类型，并可以向 IHV 扩展 DLL 提供有关通知的其他数据。

 

 





