---
title: 发送通知
description: 发送通知
ms.assetid: 55e0f41c-e042-4170-bedd-160b6c457365
keywords:
- 通知 WDK 本机 802.11 IHV 扩展 DLL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e0f5b6d471ddb1d371e654b1af25676898e7f147
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841959"
---
# <a name="sending-notifications"></a>发送通知




 

IHV 扩展 DLL 调用[**Dot11ExtSendNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_send_notification)函数将通知发送到已注册了通知的任何服务或应用程序。 若要接收通知，服务或应用程序必须通过调用 WlanRegisterNotification 函数注册到自动 Configuration Manager （ ）。 有关此功能的详细信息，请参阅 Microsoft Windows SDK 文档。

**请注意**  服务或应用程序必须注册源值为 L2\_通知\_源\_WLAN\_IHV 的通知，以便通过调用来[**接收通知。Dot11ExtSendNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_send_notification)函数。

 

调用[**Dot11ExtSendNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_send_notification)时，IHV 扩展 DLL 会将指向[**L2\_通知\_数据**](https://docs.microsoft.com/windows/desktop/api/l2cmn/ns-l2cmn-_l2_notification_data)结构的指针传递到*pNotificationData*参数。 L2\_通知\_数据定义通知的类型，并可向 IHV 扩展 DLL 提供有关通知的其他数据。

 

 





