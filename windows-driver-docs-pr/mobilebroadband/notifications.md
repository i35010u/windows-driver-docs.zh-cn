---
title: 通知
description: 通知
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f63013c0b21f3d0c72bc98560a00b28d1938d2e4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96805269"
---
# <a name="notifications"></a>通知


你可以通过服务通知来阻止你的用户，如计划激活状态、接近数据上限，以及当前漫游。 Windows 支持现有的通道，如 SMS、USSD 和 Windows 通知服务，以触发通知。

无论用户是在另一个应用中、在 " **开始** " 屏幕上，还是在桌面上，你的移动宽带应用都应该通过 toast 通知向用户传达时间关键事件。

![toast 通知](images/mb-fig3-toast.png)

您的应用程序可以接收后台事件来处理 SMS 或 USSD 通知。 有关与移动宽带应用相关联的背景通知的信息，请参阅 [windows.applicationmodel.resources.core](/uwp/api/windows.applicationmodel.background) 命名空间下的这些 API 页面：

- [MobileBroadbandDeviceServiceNotificationTrigger](/uwp/api/windows.applicationmodel.background.mobilebroadbanddeviceservicenotificationtrigger)
- [MobileBroadbandPcoDataChangeTrigger](/uwp/api/windows.applicationmodel.background.mobilebroadbandpcodatachangetrigger)
- [NetworkOperatorNotificationTrigger](/uwp/api/windows.applicationmodel.background.networkoperatornotificationtrigger)
- [SmsMessageReceivedTrigger](/uwp/api/windows.applicationmodel.background.smsmessagereceivedtrigger)

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[移动宽带应用方案](./account-management.md)

 

