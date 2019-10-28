---
title: 注册硬件配置文件更改通知
description: 注册硬件配置文件更改通知
ms.assetid: 3aaa09f7-ac63-4b56-917a-74cf344f6dd3
keywords:
- 通知 WDK PnP，硬件配置文件更改
- 硬件配置文件更改通知 WDK PnP
- EventCategoryHardwareProfileChange 通知
- 配置文件更改通知 WDK PnP
- 注册硬件配置文件更改通知
- 计算机硬件配置文件更改通知 WDK PnP
- IoRegisterPlugPlayNotification
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: e52082e4a23e7b91ffdb78d8bdee048e5419268d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838464"
---
# <a name="registering-for-hardware-profile-change-notification"></a>注册硬件配置文件更改通知





驱动程序通过调用[**IoRegisterPlugPlayNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioregisterplugplaynotification)来注册硬件配置文件更改的通知。

以下信息适用于为硬件配置文件更改通知调用此例程：

-   指定**EventCategoryHardwareProfileChange**的*EventCategory* 。

-   *EventCategoryData*必须为**NULL**。

-   如果需要，请指定 PnP 管理器将传递到回调例程的驱动程序定义的*上下文*。

驱动程序通过使用**IoRegisterPlugPlayNotification**返回的*NotificationEntry*调用[**IoUnregisterPlugPlayNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iounregisterplugplaynotification)来删除通知注册。

 

 




