---
title: 使用 PnP 硬件配置文件更改通知
description: 使用 PnP 硬件配置文件更改通知
ms.assetid: 341464e4-507d-43da-88a2-5bfecd2dd02a
keywords:
- 通知 WDK 即插即用，硬件配置文件更改
- 硬件配置文件更改通知 WDK 即插即用
- EventCategoryHardwareProfileChange 通知
- 配置文件更改通知 WDK 即插即用
- 计算机硬件配置文件更改通知 WDK 即插即用
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: ec3a9eef1121a0272ab44e5f50aba4cfd9d6df73
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391088"
---
# <a name="using-pnp-hardware-profile-change-notification"></a>使用 PnP 硬件配置文件更改通知





驱动程序注册**EventCategoryHardwareProfileChange**通知，该驱动程序可以向其通报时从一个硬件的计算机转换到另一个配置文件。 例如，驱动程序可以使用此机制插接或移除便携式计算机时收到通知。

以下各小节讨论了如何注册以进行硬件配置文件更改通知以及如何处理即插即用通知的回调例程中的硬件配置文件更改事件：

[正在注册的硬件配置文件更改通知](registering-for-hardware-profile-change-notification.md)

[处理硬件配置文件更改事件](handling-hardware-profile-change-events.md)

 

 




