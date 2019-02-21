---
title: 通知
description: 通知
ms.assetid: 55292cae-9255-4dae-9f60-93ce22253e60
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3812a8004840cf5a18ab9d017ae79a4dca91a8e7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526322"
---
# <a name="notifications"></a>通知


你可以保留用户通过如计划激活状态、 接近数据上限和当前漫游服务通知的通知。 Windows 支持短信、 USSD 和 Windows 通知服务等触发通知到的现有通道。

移动宽带应用应传达通过 toast 通知向用户的时间关键事件，无论用户是在另一个应用中，**启动**屏幕上，或在桌面上。

![toast 通知](images/mb-fig3-toast.png)

您的应用程序可以接收到进程 SMS 后台事件或 USSD 通知。 有关与移动宽带应用程序相关联的后台通知的信息，请参阅下的这些 API 页面[Windows.ApplicationModel.Background](https://docs.microsoft.com/uwp/api/windows.applicationmodel.background)命名空间：

- [MobileBroadbandDeviceServiceNotificationTrigger](https://docs.microsoft.com/uwp/api/windows.applicationmodel.background.mobilebroadbanddeviceservicenotificationtrigger)
- [MobileBroadbandPcoDataChangeTrigger](https://docs.microsoft.com/uwp/api/windows.applicationmodel.background.mobilebroadbandpcodatachangetrigger)
- [NetworkOperatorNotificationTrigger](https://docs.microsoft.com/uwp/api/windows.applicationmodel.background.networkoperatornotificationtrigger)
- [SmsMessageReceivedTrigger](https://docs.microsoft.com/uwp/api/windows.applicationmodel.background.smsmessagereceivedtrigger)

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关的主题


[移动宽带应用方案](mobile-broadband-app-scenarios.md)

 

 






