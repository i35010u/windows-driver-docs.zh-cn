---
title: 注册硬件配置文件更改通知
description: 注册硬件配置文件更改通知
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
ms.openlocfilehash: dce5a7f58605132dc4e6fd8698785f8d7dffc7d2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96793501"
---
# <a name="registering-for-hardware-profile-change-notification"></a>注册硬件配置文件更改通知





驱动程序通过调用 [**IoRegisterPlugPlayNotification**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioregisterplugplaynotification)来注册硬件配置文件更改的通知。

以下信息适用于为硬件配置文件更改通知调用此例程：

-   指定 **EventCategoryHardwareProfileChange** 的 *EventCategory* 。

-   *EventCategoryData* 必须为 **NULL**。

-   如果需要，请指定 PnP 管理器将传递到回调例程的驱动程序定义的 *上下文*。

驱动程序通过使用 **IoRegisterPlugPlayNotification** 返回的 *NotificationEntry* 调用 [**IoUnregisterPlugPlayNotification**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iounregisterplugplaynotification)来删除通知注册。

 

