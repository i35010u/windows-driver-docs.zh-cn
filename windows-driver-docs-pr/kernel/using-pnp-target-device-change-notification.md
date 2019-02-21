---
title: 使用即插即用的目标设备更改通知
description: 使用即插即用的目标设备更改通知
ms.assetid: a56bda5c-e398-442d-bc90-2e63f8f7e6bf
keywords:
- 通知 WDK 即插即用，目标设备更改
- 目标设备更改通知 WDK 即插即用
- EventCategoryTargetDeviceChange 通知
ms.date: 10/30/2018
ms.localizationpriority: medium
ms.openlocfilehash: 1ec75ef243cc1b8dd7f6b6bb6dda05a4dc84ba3b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526529"
---
# <a name="using-pnp-target-device-change-notification"></a>使用即插即用的目标设备更改通知

驱动程序注册**EventCategoryTargetDeviceChange** ，驱动程序可以向其通报将要移除设备时在设备上的通知。 例如，如果驱动程序将打开到设备的句柄，该驱动程序应注册，以便**EventCategoryTargetDeviceChange**因此驱动程序可以关闭其句柄，当需要删除该设备的即插即用的管理器时在设备上的通知。

驱动程序还可以使用**EventCategoryTargetDeviceChange**自定义通知的通知。 (请参阅[使用即插即用的自定义通知](using-pnp-custom-notification.md)。)

> [!IMPORTANT]
> 即插即用的目标设备更改通知注册不是以通知有关目标设备电源状态更改的侦听器。 如果驱动程序需要知道有关目标设备电源更改，该驱动程序应改为定义之间的设备的 power 关系。 
>
> 若要定义 power 关系，驱动程序调用[ **IoInvalidateDeviceRelations** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioinvalidatedevicerelations)与*类型*参数设置为**PowerRelations**，然后为 PnP 管理器的响应[IRP_MN_QUERY_DEVICE_RELATIONS](irp-mn-query-device-relations.md)查询**PowerRelations**使用正确的信息。

以下各小节讨论了如何注册目标设备更改通知以及如何处理目标设备的即插即用通知回调例程中的更改事件：

[正在注册的目标设备更改通知](registering-for-target-device-change-notification.md)

[处理一个 GUID\_目标\_设备\_查询\_删除事件](handling-a-guid-target-device-query-remove-event.md)

[处理一个 GUID\_目标\_设备\_删除\_完成事件](handling-a-guid-target-device-remove-complete-event.md)

[处理一个 GUID\_目标\_设备\_删除\_已取消事件](handling-a-guid-target-device-remove-cancelled-event.md)

 

 




