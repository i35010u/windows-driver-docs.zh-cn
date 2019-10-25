---
title: 使用 PnP 设备接口更改通知
description: 使用 PnP 设备接口更改通知
ms.assetid: 2ed3518a-601f-4e9b-b375-a9fb62c937a9
keywords:
- 通知 WDK PnP，设备接口更改
- EventCategoryDeviceInterfaceChange 通知
- 设备接口更改通知 WDK PnP
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0b69a5e4fa089a4b02cff69ea6386d8406c909d3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835880"
---
# <a name="using-pnp-device-interface-change-notification"></a>使用 PnP 设备接口更改通知





驱动程序注册**EventCategoryDeviceInterfaceChange**通知，以便当特定类的设备接口到达（已启用）或在计算机上被删除（禁用）时，可以通知该驱动程序。 例如，复合电池驱动程序可能会注册类电池的设备接口通知，因此它可以向操作系统提供有关可用电池电量总计的信息。

以下小节讨论了如何注册设备接口更改通知，以及如何在 PnP 通知回调例程中处理设备接口更改事件：

[注册设备接口更改通知](registering-for-device-interface-change-notification.md)

[处理设备接口更改事件](handling-device-interface-change-events.md)

有关设备接口的信息，请参阅[**IoRegisterDeviceInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioregisterdeviceinterface)和相关例程。

 

 




