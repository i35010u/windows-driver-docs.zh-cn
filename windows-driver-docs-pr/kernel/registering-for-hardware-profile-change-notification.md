---
title: 注册硬件配置文件更改通知
description: 注册硬件配置文件更改通知
ms.assetid: 3aaa09f7-ac63-4b56-917a-74cf344f6dd3
keywords:
- 通知 WDK 即插即用，硬件配置文件更改
- 硬件配置文件更改通知 WDK 即插即用
- EventCategoryHardwareProfileChange 通知
- 配置文件更改通知 WDK 即插即用
- 注册硬件配置文件更改通知
- 计算机硬件配置文件更改通知 WDK 即插即用
- IoRegisterPlugPlayNotification
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 11ad18adc1ac01f59c8aaa6ec9f30eed7d503624
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63338444"
---
# <a name="registering-for-hardware-profile-change-notification"></a>注册硬件配置文件更改通知





驱动程序通过调用注册的硬件配置文件更改通知[ **IoRegisterPlugPlayNotification**](https://msdn.microsoft.com/library/windows/hardware/ff549526)。

以下信息适用于硬件配置文件更改通知才能调用该例程：

-   指定*EventCategory*的**EventCategoryHardwareProfileChange**。

-   *EventCategoryData*必须是**NULL**。

-   指定驱动程序定义*上下文*，如果合适，即插即用管理器将传递给回调例程。

驱动程序通过调用来消除通知注册[ **IoUnregisterPlugPlayNotification** ](https://msdn.microsoft.com/library/windows/hardware/ff550398)与*NotificationEntry*返回的**IoRegisterPlugPlayNotification**。

 

 




