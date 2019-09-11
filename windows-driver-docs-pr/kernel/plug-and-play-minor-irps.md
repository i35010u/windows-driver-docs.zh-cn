---
title: 即插即用次要 IRP
description: 即插即用次要 IRP
ms.date: 08/12/2017
ms.assetid: eeb7dafd-fb44-4fb7-b5f0-314059ee0093
ms.localizationpriority: medium
ms.openlocfilehash: 356aa08a1c06571a401545050b93de0caa87721c
ms.sourcegitcommit: 9b0ddcdba8c56987b45e538948b2ac8c60ef1287
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/10/2019
ms.locfileid: "70876929"
---
# <a name="plug-and-play-minor-irps"></a>即插即用次要 IRP





本部分介绍发送到驱动程序的 PnP Irp。 所有 PnP irp 都具有主函数代码[**IRP\_MJ\_PnP**](irp-mj-pnp.md)和用于指示特定 PnP 请求的次要函数代码。

本部分提供单个 Irp 的参考信息。 有关 Irp 发送顺序的说明，请参阅[即插即用](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-plug-and-play)，有关如何处理 irp 的详细[说明，请](https://docs.microsoft.com/windows-hardware/drivers/kernel/dispatchpnp-routines)参阅 PnP 概念和术语的常规讨论。

对于每个 IRP 和每种类型的驱动程序，需要使用驱动程序来处理 IRP，还可以选择处理 IRP，或者不得处理 IRP。 请参阅下表以确定驱动程序将处理哪些 Irp，然后查阅参考页获取有关各个 Irp 的信息。 Irp 按功能顺序列出在表中，并在 IRP 引用页中按字母顺序列出。

如果某个特定驱动程序的表中的 IRP 标记为 "否"，则该驱动程序不得处理 IRP。 驱动程序必须将 IRP 传递到设备堆栈中的下一个驱动程序，如 IRP 的参考页中所述。

PnP 管理器发送这些 Irp。 PnP 驱动程序可以发送其中一些 Irp，但只有在此部分中进行了说明。

下面是 PnP Irp 的次要函数代码和处理它们的驱动程序类型：


|                              PnP IRP 次要函数代码                              | Nonbus 设备的函数或筛选器驱动程序 | 总线设备的函数驱动程序（适用于总线 FDO） | 总线驱动程序或总线筛选器驱动程序（对于子 PDOs） |
|---------------------------------------------------------------------------------------|---------------------------------------------|----------------------------------------------|--------------------------------------------------|
|                 [**IRP\_MN\_启动设备\_** ](irp-mn-start-device.md)                  |                  必填                   |                   必填                   |                     必填                     |
|            [**IRP\_MN\_查询停止\_设备\_** ](irp-mn-query-stop-device.md)            |                  必需                   |                   必填                   |                     必填                     |
|                  [**IRP\_MN\_停止设备\_** ](irp-mn-stop-device.md)                   |                  必填                   |                   必填                   |                     必填                     |
|           [**IRP\_MN\_取消停止\_设备\_** ](irp-mn-cancel-stop-device.md)           |                  必需                   |                   必填                   |                     必填                     |
|          [**IRP\_MN\_查询删除\_设备\_** ](irp-mn-query-remove-device.md)          |                  必填                   |                   必填                   |                     必填                     |
|                [**IRP\_MN\_删除设备\_** ](irp-mn-remove-device.md)                 |                  必需                   |                   必需                   |                     必填                     |
|         [**IRP\_MN\_取消删除\_设备\_** ](irp-mn-cancel-remove-device.md)         |                  必需                   |                   必填                   |                     必填                     |
|             [**IRP\_MN\_意外删除\_** ](irp-mn-surprise-removal.md)              |                  必需                   |                   必填                   |                     必需                     |
|           [**IRP\_MN\_查询功能\_** ](irp-mn-query-capabilities.md)            |                  可选                   |              可选 | 必填               |                                                  |
|      [**IRP\_MN\_查询\_PNP设备状态\_\_** ](irp-mn-query-pnp-device-state.md)       |                  可选                   |                   可选                   |                     可选                     |
| [**IRP\_MN\_筛选器\_资源要求\_** ](irp-mn-filter-resource-requirements.md) |                可选（1）                 |                 可选（1）                 |                        否                        |
|    [**IRP\_MN\_设备使用\_通知\_** ](irp-mn-device-usage-notification.md)    |                必需（1）                 |                 必需（1）                 |                   必需（1）                   |
|       [**IRP\_MN\_查询设备\_关系\_** ](irp-mn-query-device-relations.md)       |                                             |                                              |                                                  |
|                                 -   **BusRelations**                                  |                可选（1）                 |                   必填                   |                      否（2）                      |
|                               -   **EjectionRelations**                               |                     否                      |                      否                      |                     可选                     |
|                               -   **RemovalRelations**                                |                  可选                   |                   可选                   |                        否                        |
|                             -   **TargetDeviceRelation**                              |                     否                      |                      否                      |                     必填                     |
|              [**IRP\_MN\_查询资源\_** ](irp-mn-query-resources.md)               |                     否                      |                      否                      |                   必需（1）                   |
|  [**IRP\_MN\_查询资源\_需求\_** ](irp-mn-query-resource-requirements.md)  |                     否                      |                      否                      |                   必需（1）                   |
|                     [**IRP\_MN\_查询ID\_** ](irp-mn-query-id.md)                      |                                             |                                              |                                                  |
|                               -   **BusQueryDeviceID**                                |                     否                      |                      否                      |                     必需                     |
|                              -   **BusQueryHardwareIDs**                              |                     否                      |                      否                      |                     可选                     |
|                             -   **BusQueryCompatibleIDs**                             |                     否                      |                  否  |  可选                  |                                                  |
|                              -   **BusQueryInstanceID**                               |                     否                      |                      否                      |                     可选                     |
|                              -   **BusQueryContainerID**                              |                     否                      |                      否                      |                   必需（3）                   |
|            [**IRP\_MN\_查询设备\_文本\_** ](irp-mn-query-device-text.md)            |                     否                      |                      否                      |                   必需（1）                   |
|        [**IRP\_MN\_查询总线\_信息\_** ](irp-mn-query-bus-information.md)        |                     否                      |                      否                      |                   必需（1）                   |
|              [**IRP\_MN\_查询接口\_** ](irp-mn-query-interface.md)               |                  可选                   |                   可选                   |                   必需（1）                   |
|                  [**IRP\_MN\_读取配置\_** ](irp-mn-read-config.md)                   |                     否                      |                      否                      |                   必需（1）                   |
|                 [**IRP\_MN\_写入配置\_** ](irp-mn-write-config.md)                  |                     否                      |                      否                      |                   必需（1）                   |
|            [**IRP\_MN\_设备\_已枚举**](irp-mn-device-enumerated.md)             |                     否                      |                      否                      |                   必需（1）                   |
|                     [**IRP\_MN\_设置锁定\_** ](irp-mn-set-lock.md)                      |                     否                      |                      否                      |                   必需（1）                   |

（1）在某些情况下是必需的或可选的。 有关更多详细信息，请参阅 IRP 的参考页。

（2）总线筛选器驱动程序可能会处理**BusRelations**的查询。

（3）在 windows 7 和更高版本的 Windows 中受支持。










