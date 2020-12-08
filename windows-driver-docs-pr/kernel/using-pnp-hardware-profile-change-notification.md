---
title: 使用 PnP 硬件配置文件更改通知
description: 使用 PnP 硬件配置文件更改通知
keywords:
- 通知 WDK PnP，硬件配置文件更改
- 硬件配置文件更改通知 WDK PnP
- EventCategoryHardwareProfileChange 通知
- 配置文件更改通知 WDK PnP
- 计算机硬件配置文件更改通知 WDK PnP
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: f3061cb810d674feb031715a0860b3631c9c4ac3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96816037"
---
# <a name="using-pnp-hardware-profile-change-notification"></a>使用 PnP 硬件配置文件更改通知





驱动程序注册 **EventCategoryHardwareProfileChange** 通知，以便在计算机从一个硬件配置文件转换到另一个硬件配置文件时，通知该驱动程序。 例如，驱动程序可以使用此机制在便携式计算机插接或取消插接时收到通知。

以下小节讨论了如何注册硬件配置文件更改通知，以及如何在 PnP 通知回调例程中处理硬件配置文件更改事件：

[注册硬件配置文件更改通知](registering-for-hardware-profile-change-notification.md)

[处理硬件配置文件更改事件](handling-hardware-profile-change-events.md)

 

 




