---
title: 使用 PnP 设备接口更改通知
description: 使用 PnP 设备接口更改通知
ms.assetid: 2ed3518a-601f-4e9b-b375-a9fb62c937a9
keywords:
- 通知 WDK 即插即用设备接口更改
- EventCategoryDeviceInterfaceChange 通知
- 设备接口更改通知 WDK 即插即用
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5b584bfdeeae4d3c46cb2389a2d5448e62efc619
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391070"
---
# <a name="using-pnp-device-interface-change-notification"></a>使用 PnP 设备接口更改通知





驱动程序注册**EventCategoryDeviceInterfaceChange**通知以便为特定类的设备接口到达时，可以通知驱动程序 （已启用） 或在计算机上的已删除 （禁用）。 例如，复合电池驱动程序可能会注册通知的设备接口的类电池以便它可以提供给系统总可用电池电源有关的信息。

以下各小节讨论了如何注册设备接口更改通知以及如何处理即插即用通知的回调例程中的设备接口更改事件：

[正在注册的设备接口更改通知](registering-for-device-interface-change-notification.md)

[处理设备接口更改事件](handling-device-interface-change-events.md)

请参阅[ **IoRegisterDeviceInterface** ](https://msdn.microsoft.com/library/windows/hardware/ff549506)和相关的例程的有关设备接口的信息。

 

 




