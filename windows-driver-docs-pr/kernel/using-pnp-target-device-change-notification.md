---
title: 使用 PnP 目标设备更改通知
description: 使用 PnP 目标设备更改通知
ms.assetid: a56bda5c-e398-442d-bc90-2e63f8f7e6bf
keywords:
- 通知 WDK PnP，目标设备更改
- 目标设备更改通知 WDK PnP
- EventCategoryTargetDeviceChange 通知
ms.date: 10/30/2018
ms.localizationpriority: medium
ms.openlocfilehash: 65469d49ff534c95ac26f052b2fdc42cac8a99b9
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89183993"
---
# <a name="using-pnp-target-device-change-notification"></a>使用 PnP 目标设备更改通知

驱动程序在设备上注册 **EventCategoryTargetDeviceChange** 通知，以便在删除设备时可以通知该驱动程序。 例如，如果驱动程序打开设备的句柄，则驱动程序应在设备上注册 **EventCategoryTargetDeviceChange** 通知，以便在 PnP 管理器需要删除设备时，驱动程序可以关闭其句柄。

驱动程序还可以将 **EventCategoryTargetDeviceChange** 通知用于自定义通知。  (参阅 [使用 PnP 自定义通知](using-pnp-custom-notification.md)。 ) 

> [!IMPORTANT]
> 注册 PnP 目标设备更改通知并不旨在通知侦听器有关目标设备电源状态更改的信息。 如果驱动程序需要了解目标设备的电源更改，则驱动程序应改为定义设备之间的电源关系。 
>
> 若要定义电源关系，驱动程序将调用 [**IoInvalidateDeviceRelations**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioinvalidatedevicerelations) ，并将 *Type* 参数设置为 **PowerRelations**，然后使用正确的信息响应 PnP 经理 [IRP_MN_QUERY_DEVICE_RELATIONS](irp-mn-query-device-relations.md) 对 **PowerRelations** 的查询。

以下小节讨论了如何注册目标设备更改通知，以及如何在 PnP 通知回调例程中处理目标设备更改事件：

[注册目标设备更改通知](registering-for-target-device-change-notification.md)

[处理 GUID \_ 目标 \_ 设备 \_ 查询 \_ 删除事件](handling-a-guid-target-device-query-remove-event.md)

[处理 GUID \_ 目标 \_ 设备 \_ 删除 \_ 完成事件](handling-a-guid-target-device-remove-complete-event.md)

[处理 GUID \_ 目标 \_ 设备删除 \_ 已 \_ 取消事件](handling-a-guid-target-device-remove-cancelled-event.md)

 

