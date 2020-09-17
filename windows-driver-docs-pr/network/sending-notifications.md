---
title: 发送通知
description: 发送通知
ms.assetid: 55e0f41c-e042-4170-bedd-160b6c457365
keywords:
- 通知 WDK 本机 802.11 IHV 扩展 DLL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a02a1f815c42002824a832a43fd3945810b1e316
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90715042"
---
# <a name="sending-notifications"></a>发送通知




 

IHV 扩展 DLL 调用 [**Dot11ExtSendNotification**](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_send_notification) 函数将通知发送到已注册了通知的任何服务或应用程序。 若要接收通知，服务或应用程序必须通过调用 **WlanRegisterNotification** 函数，注册到自动 Configuration Manager () 。 有关此功能的详细信息，请参阅 Microsoft Windows SDK 文档。

**注意**   服务或应用程序必须注册源值为 L2 \_ 通知源 WLAN IHV 的通知，以便 \_ \_ \_ 通过调用[**Dot11ExtSendNotification**](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_send_notification)函数接收通知。

 

调用 [**Dot11ExtSendNotification**](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_send_notification)时，IHV 扩展 DLL 会将指向 [**L2 \_ 通知 \_ 数据**](/windows/win32/api/l2cmn/ns-l2cmn-_l2_notification_data) 结构的指针传递到 *pNotificationData* 参数。 L2 \_ 通知 \_ 数据定义通知的类型，并可向 IHV 扩展 DLL 提供有关通知的其他数据。

 

 