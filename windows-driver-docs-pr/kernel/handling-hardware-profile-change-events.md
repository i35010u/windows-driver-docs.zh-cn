---
title: 处理硬件配置文件更改事件
description: 处理硬件配置文件更改事件
ms.assetid: ddb0f740-9b31-4ede-be84-c1f6eb60fb1a
keywords:
- 通知 WDK 即插即用，硬件配置文件更改
- 硬件配置文件更改通知 WDK 即插即用
- EventCategoryHardwareProfileChange 通知
- 配置文件更改通知 WDK 即插即用
- 计算机硬件配置文件更改通知 WDK 即插即用
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2c51c44adca1a78b837af2582230d031d3a803b5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63359381"
---
# <a name="handling-hardware-profile-change-events"></a>处理硬件配置文件更改事件





更改硬件配置文件中的特定时间，即插即用管理器调用通知为注册的回调例程**EventCategoryHardwareProfileChange**:

-   PnP 管理器计算机的硬件配置文件中的更改之前，调用回调例程的已注册的通知，并指定*NotificationStructure*。**事件**的 GUID\_HWPROFILE\_查询\_更改。

-   计算机的硬件配置文件更改完成后，即插即用管理器调用回调例程的已注册的通知，并指定*NotificationStructure*。**事件**的 GUID\_HWPROFILE\_更改\_完成。

-   如果计算机的硬件配置文件更改已取消，PnP 管理器调用回调例程的已注册的通知，并指定*NotificationStructure*。**事件**的 GUID\_HWPROFILE\_更改\_已取消。

对于 GUID\_HWPROFILE\_查询\_更改事件的即插即用的管理器调用回调例程的用户模式下，，然后调用内核模式回调例程。 以响应一个 GUID\_HWPROFILE\_查询\_更改事件驱动程序的通知回调例程通常只需将返回状态\_成功。

对于 GUID\_HWPROFILE\_更改\_完成事件的即插即用的管理器调用回调例程的内核模式下，，然后调用用户模式回调例程。 在响应这种情况下，驱动程序的回调例程可能会刷新其硬件配置文件特定的设置。

对于 GUID\_HWPROFILE\_更改\_已取消事件的即插即用的管理器将调用内核模式回调例程，然后用户模式下例程。 在响应这种情况下，驱动程序的回调例程通常只需返回状态\_成功。 如果驱动程序执行任何操作以响应 GUID\_HWPROFILE\_查询\_更改事件，该驱动程序则会撤消这些操作以响应取消事件。

 

 




