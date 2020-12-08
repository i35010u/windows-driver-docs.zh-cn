---
title: 处理硬件配置文件更改事件
description: 处理硬件配置文件更改事件
keywords:
- 通知 WDK PnP，硬件配置文件更改
- 硬件配置文件更改通知 WDK PnP
- EventCategoryHardwareProfileChange 通知
- 配置文件更改通知 WDK PnP
- 计算机硬件配置文件更改通知 WDK PnP
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: a0d71fe3547d5559361c9a6bf48b841c281c8d85
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96836411"
---
# <a name="handling-hardware-profile-change-events"></a>处理硬件配置文件更改事件





在硬件配置文件更改期间的特定时间，PnP 管理器会调用为 **EventCategoryHardwareProfileChange** 注册的通知回调例程：

-   在计算机的硬件配置文件中发生更改之前，PnP 管理器会调用注册的通知回调例程并指定 *NotificationStructure*。**Event** GUID \_ hwprofile 中 \_ 查询更改的事件 \_ 。

-   计算机的硬件配置文件更改完成后，PnP 管理器将调用注册的通知回调例程并指定 *NotificationStructure*。**Event** GUID \_ hwprofile 中 \_ 更改完成的事件 \_ 。

-   如果计算机的硬件配置文件更改已取消，则 PnP 管理器会调用注册的通知回调例程，并指定 *NotificationStructure*。GUID hwprofile 中更改的 **事件** 已 \_ \_ \_ 取消。

对于 GUID \_ hwprofile 中 \_ 查询 \_ 更改事件，PnP 管理器调用用户模式回调例程，然后调用内核模式回调例程。 为了响应 GUID \_ hwprofile 中 \_ 查询 \_ 更改事件，驱动程序的通知回调例程通常只返回状态 " \_ 成功"。

对于 GUID \_ hwprofile 中 \_ CHANGE \_ 完成事件，PnP 管理器调用内核模式回调例程，然后调用用户模式回调例程。 为了响应此类事件，驱动程序的回调例程可能会刷新其特定于硬件配置文件的设置。

对于 GUID \_ hwprofile 中 \_ 更改已 \_ 取消事件，PnP 管理器会调用内核模式回调例程，然后调用用户模式例程。 作为此类事件的响应，驱动程序的回调例程通常只返回状态 " \_ 成功"。 如果驱动程序执行了任何操作来响应 GUID \_ hwprofile 中 \_ QUERY \_ CHANGE 事件，则驱动程序会在响应取消事件时撤消这些操作。

 

 




