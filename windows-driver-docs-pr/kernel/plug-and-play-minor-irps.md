---
title: 即插即用次要 IRP
description: 即插即用次要 IRP
ms.date: 08/12/2017
ms.assetid: eeb7dafd-fb44-4fb7-b5f0-314059ee0093
ms.localizationpriority: medium
ms.openlocfilehash: 559e226036022cc7c04b91a0422798c1d490d585
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380943"
---
# <a name="plug-and-play-minor-irps"></a>即插即用次要 IRP





本部分介绍了发送到驱动程序 PnP Irp。 所有 PnP Irp 具有主要函数代码[ **IRP\_MJ\_PNP** ](irp-mj-pnp.md)和一个次要函数代码，指示特定的即插即用请求。

本部分提供有关各个 Irp 的参考信息。 请参阅[插](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-plug-and-play)Irp 发送的顺序，讨论了如何处理 Irp 中的说明[DispatchPnP 例程](https://docs.microsoft.com/windows-hardware/drivers/kernel/dispatchpnp-routines)，和常规讨论的即插即用的概念和术语。

对于每个 IRP 和每种类型的驱动程序，驱动程序是处理 IRP，所需的任何一个可以根据需要处理 IRP，或必须处理 IRP。 请参考下表以确定哪些 Irp 您的驱动程序将处理并请查阅有关单个 Irp 信息的参考页。 中的表和 IRP 参考页中按字母顺序的功能顺序列出了 Irp。

如果 IRP 标记为"否"的特定驱动程序的表中，该驱动程序必须处理 IRP。 该驱动程序必须将 IRP 传递给设备堆栈中所述的参考页的 IRP 中的下一步驱动程序。

PnP 管理器将这些发送 Irp。 即插即用驱动程序可以发送一些这些 Irp，而只能在本部分中相应说明。

PnP Irp 和处理它们的驱动程序类型的小函数代码如下：


|                              PnP IRP 次要函数代码                              | Nonbus 设备函数或筛选器驱动程序 | 函数 （代表公交 FDO） 的总线设备驱动程序 | 总线驱动程序或总线筛选器驱动程序 （适用于子 PDOs) |
|---------------------------------------------------------------------------------------|---------------------------------------------|----------------------------------------------|--------------------------------------------------|
|                 [**IRP\_MN\_START\_DEVICE**](irp-mn-start-device.md)                  |                  必需                   |                   必需                   |                     必需                     |
|            [**IRP\_MN\_查询\_停止\_设备**](irp-mn-query-stop-device.md)            |                  必需                   |                   必需                   |                     必需                     |
|                  [**IRP\_MN\_STOP\_DEVICE**](irp-mn-stop-device.md)                   |                  必需                   |                   必需                   |                     必需                     |
|           [**IRP\_MN\_CANCEL\_STOP\_DEVICE**](irp-mn-cancel-stop-device.md)           |                  必需                   |                   必需                   |                     必需                     |
|          [**IRP\_MN\_查询\_删除\_设备**](irp-mn-query-remove-device.md)          |                  必需                   |                   必需                   |                     必需                     |
|                [**IRP\_MN\_REMOVE\_DEVICE**](irp-mn-remove-device.md)                 |                  必需                   |                   必需                   |                     必需                     |
|         [**IRP\_MN\_CANCEL\_REMOVE\_DEVICE**](irp-mn-cancel-remove-device.md)         |                  必需                   |                   必需                   |                     必需                     |
|             [**IRP\_MN\_SURPRISE\_REMOVAL**](irp-mn-surprise-removal.md)              |                  必需                   |                   必需                   |                     必需                     |
|           [**IRP\_MN\_查询\_功能**](irp-mn-query-capabilities.md)            |                  可选                   |              可选的所需               |                                                  |
|      [**IRP\_MN\_QUERY\_PNP\_DEVICE\_STATE**](irp-mn-query-pnp-device-state.md)       |                  可选                   |                   可选                   |                     可选                     |
| [**IRP\_MN\_FILTER\_RESOURCE\_REQUIREMENTS**](irp-mn-filter-resource-requirements.md) |                可选 (1)                 |                 可选 (1)                 |                        否                        |
|    [**IRP\_MN\_DEVICE\_USAGE\_NOTIFICATION**](irp-mn-device-usage-notification.md)    |                必需 (1)                 |                 必需 (1)                 |                   必需 (1)                   |
|       [**IRP\_MN\_查询\_设备\_关系**](irp-mn-query-device-relations.md)       |                                             |                                              |                                                  |
|                                 -   **BusRelations**                                  |                可选 (1)                 |                   必需                   |                      否 （2)                      |
|                               -   **EjectionRelations**                               |                     否                      |                      否                      |                     可选                     |
|                               -   **RemovalRelations**                                |                  可选                   |                   可选                   |                        否                        |
|                             -   **TargetDeviceRelation**                              |                     否                      |                      否                      |                     必需                     |
|              [**IRP\_MN\_查询\_资源**](irp-mn-query-resources.md)               |                     否                      |                      否                      |                   必需 (1)                   |
|  [**IRP\_MN\_查询\_资源\_要求**](irp-mn-query-resource-requirements.md)  |                     否                      |                      否                      |                   必需 (1)                   |
|                     [**IRP\_MN\_查询\_ID**](irp-mn-query-id.md)                      |                                             |                                              |                                                  |
|                               -   **BusQueryDeviceID**                                |                     否                      |                      否                      |                     必需                     |
|                              -   **BusQueryHardwareIDs**                              |                     否                      |                      否                      |                     可选                     |
|                             -   **BusQueryCompatibleIDs**                             |                     否                      |                  NoOptional                  |                                                  |
|                              -   **BusQueryInstanceID**                               |                     否                      |                      否                      |                     可选                     |
|                              -   **BusQueryContainerID**                              |                     否                      |                      否                      |                   必需 (3)                   |
|            [**IRP\_MN\_QUERY\_DEVICE\_TEXT**](irp-mn-query-device-text.md)            |                     否                      |                      否                      |                   必需 (1)                   |
|        [**IRP\_MN\_查询\_总线\_信息**](irp-mn-query-bus-information.md)        |                     否                      |                      否                      |                   必需 (1)                   |
|              [**IRP\_MN\_查询\_接口**](irp-mn-query-interface.md)               |                  可选                   |                   可选                   |                   必需 (1)                   |
|                  [**IRP\_MN\_READ\_CONFIG**](irp-mn-read-config.md)                   |                     否                      |                      否                      |                   必需 (1)                   |
|                 [**IRP\_MN\_WRITE\_CONFIG**](irp-mn-write-config.md)                  |                     否                      |                      否                      |                   必需 (1)                   |
|            [**IRP\_MN\_DEVICE\_ENUMERATED**](irp-mn-device-enumerated.md)             |                     否                      |                      否                      |                   必需 (1)                   |
|                     [**IRP\_MN\_SET\_LOCK**](irp-mn-set-lock.md)                      |                     否                      |                      否                      |                   必需 (1)                   |

（1） 必需或可选在某些情况下。 IRP 的更多详细信息，请参阅参考页。

（2） 总线筛选器驱动程序可能会处理的查询**BusRelations**。

（3） 在 Windows 7 和更高版本的 Windows 中受支持。










