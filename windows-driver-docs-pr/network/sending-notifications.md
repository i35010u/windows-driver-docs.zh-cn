---
title: 发送通知
description: 发送通知
ms.assetid: 55e0f41c-e042-4170-bedd-160b6c457365
keywords:
- 通知 WDK 本机 802.11 IHV 扩展 DLL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c9276a00994d69b780530158efc6214c78596195
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56569023"
---
# <a name="sending-notifications"></a>发送通知




 

IHV 扩展 DLL 调用[ **Dot11ExtSendNotification** ](https://msdn.microsoft.com/library/windows/hardware/ff547560)函数将通知发送到任何服务或应用程序已注册的通知。 若要接收通知，服务或应用程序必须注册使用自动配置管理器 (ACM) 通过调用**WlanRegisterNotification**函数。 有关此函数的详细信息，请参阅 Microsoft Windows SDK 文档。

**请注意**  服务或应用程序必须使用注册通知的源值的 L2\_通知\_源\_WLAN\_IHV 才能通过接收通知调用[ **Dot11ExtSendNotification** ](https://msdn.microsoft.com/library/windows/hardware/ff547560)函数。

 

调用时[ **Dot11ExtSendNotification**](https://msdn.microsoft.com/library/windows/hardware/ff547560)，IHV 扩展 DLL 将传递一个指向[ **L2\_通知\_数据**](https://msdn.microsoft.com/library/windows/hardware/ff557044)结构*pNotificationData*参数。 L2\_通知\_数据定义通知的类型，并可以向 IHV 扩展 DLL 提供有关通知的其他数据。

 

 





