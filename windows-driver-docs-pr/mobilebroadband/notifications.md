---
title: 通知
description: 通知
ms.assetid: 55292cae-9255-4dae-9f60-93ce22253e60
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 11dae23205e6b0f7a447434bbfcfd3d4988702a1
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89217838"
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

 

