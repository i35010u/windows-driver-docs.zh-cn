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
ms.openlocfilehash: 42a9cdf287197f4676f4d0461a685fa80c13645a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373461"
---
# <a name="registering-for-hardware-profile-change-notification"></a>注册硬件配置文件更改通知





驱动程序通过调用注册的硬件配置文件更改通知[ **IoRegisterPlugPlayNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioregisterplugplaynotification)。

以下信息适用于硬件配置文件更改通知才能调用该例程：

-   指定*EventCategory*的**EventCategoryHardwareProfileChange**。

-   *EventCategoryData*必须是**NULL**。

-   指定驱动程序定义*上下文*，如果合适，即插即用管理器将传递给回调例程。

驱动程序通过调用来消除通知注册[ **IoUnregisterPlugPlayNotification** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iounregisterplugplaynotification)与*NotificationEntry*返回的**IoRegisterPlugPlayNotification**。

 

 




