---
title: 即插即用次要 IRP
description: 即插即用次要 IRP
ms.date: 08/12/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9541f8ef25d70b08b474a9e7624e7af9d97fd723
ms.sourcegitcommit: 5524e265f46836100be5fb36ca6fdcac488ab274
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/13/2021
ms.locfileid: "103417244"
---
# <a name="plug-and-play-minor-irps"></a>即插即用次要 IRP





本部分介绍发送到驱动程序的 PnP Irp。 所有 PnP Irp 都具有主函数代码 [**IRP \_ MJ \_ PnP**](irp-mj-pnp.md) 和用于指示特定 PnP 请求的次要函数代码。

本部分提供单个 Irp 的参考信息。 有关 Irp 发送顺序的说明，请参阅 [即插即用](./introduction-to-plug-and-play.md) ，有关如何处理 irp 的详细 [说明，请](./dispatchpnp-routines.md)参阅 PnP 概念和术语的常规讨论。

对于每个 IRP 和每种类型的驱动程序，需要使用驱动程序来处理 IRP，还可以选择处理 IRP，或者不得处理 IRP。 请参阅下表以确定驱动程序将处理哪些 Irp，然后查阅参考页获取有关各个 Irp 的信息。 Irp 按功能顺序列出在表中，并在 IRP 引用页中按字母顺序列出。

如果某个特定驱动程序的表中的 IRP 标记为 "否"，则该驱动程序不得处理 IRP。 驱动程序必须将 IRP 传递到设备堆栈中的下一个驱动程序，如 IRP 的参考页中所述。

PnP 管理器发送这些 Irp。 PnP 驱动程序可以发送其中一些 Irp，但只有在此部分中进行了说明。

下面是 PnP Irp 的次要函数代码和处理它们的驱动程序类型：


|                              PnP IRP 次要函数代码                              | 值 | Nonbus 设备的函数或筛选器驱动程序 | 用于 bus FDO) 的总线设备 (的函数驱动程序 |  (子 PDOs) 的总线驱动程序或总线筛选器驱动程序 |
|---------------------------------------------------------------------------------------|---------------------------------------------|----------------------------------------------|--------------------------------------------------|---|
|                 [**IRP \_ MN \_ 启动 \_ 设备**](irp-mn-start-device.md)                  |0x00|                  必选                   |                   必选                   |                     必选                     |
|          [**IRP \_ MN \_ 查询 \_ 删除 \_ 设备**](irp-mn-query-remove-device.md)          |0x01|                  必选                   |                   必选                   |                     必选                     |
|                [**IRP \_ MN \_ 删除 \_ 设备**](irp-mn-remove-device.md)                 |0x02|                  必选                   |                   必选                   |                     必选                     |
|         [**IRP \_ MN \_ 取消 \_ 删除 \_ 设备**](irp-mn-cancel-remove-device.md)         |0x03|                  必选                   |                   必选                   |                     必选                     |
|                  [**IRP \_ MN \_ 停止 \_ 设备**](irp-mn-stop-device.md)                   |0x04|                  必选                   |                   必选                   |                     必选                     |
|            [**IRP \_ MN \_ 查询 \_ 停止 \_ 设备**](irp-mn-query-stop-device.md)            |0x05|                  必选                   |                   必选                   |                     必选                     |
|           [**IRP \_ MN \_ 取消 \_ 停止 \_ 设备**](irp-mn-cancel-stop-device.md)           |0x06|                  必选                   |                   必选                   |                     必选                     |
|       [**IRP \_ MN \_ 查询 \_ 设备 \_ 关系**](irp-mn-query-device-relations.md)       |0x07                                             |                                              |                                                  |
|                                 -   **BusRelations**                                  |x|                可选 (1)                  |                   必选                   |                      无 (2)                       |
|                               -   **EjectionRelations**                               |x|                     否                      |                      否                      |                     可选                     |
|                               -   **RemovalRelations**                                |x|                  可选                   |                   可选                   |                        否                        |
|                             -   **TargetDeviceRelation**                              |x|                     否                      |                      否                      |                     必需                     |
|              [**IRP \_ MN \_ 查询 \_ 接口**](irp-mn-query-interface.md)               |0x08|                  可选                   |                   可选                   |                   必需 (1)                    |
|           [**IRP \_ MN \_ 查询 \_ 功能**](irp-mn-query-capabilities.md)            |0x09|                  可选                   |              可选 | 必需               |                                                  |
|              [**IRP \_ MN \_ 查询 \_ 资源**](irp-mn-query-resources.md)               |0x0A|                     否                      |                      否                      |                   必需 (1)                    |
|  [**IRP \_ MN \_ 查询 \_ 资源 \_ 需求**](irp-mn-query-resource-requirements.md)  |0x0B|                     否                      |                      否                      |                   必需 (1)                    |
|            [**IRP \_ MN \_ 查询 \_ 设备 \_ 文本**](irp-mn-query-device-text.md)            |0x0C|                     否                      |                      否                      |                   必需 (1)                    |
| [**IRP \_ MN \_ 筛选器 \_ 资源 \_ 要求**](irp-mn-filter-resource-requirements.md) |0x0D|                可选 (1)                  |                 可选 (1)                  |                        否                        |
|                  [**IRP \_ MN \_ 读取 \_ 配置**](irp-mn-read-config.md)                   |0x0F|                     否                      |                      否                      |                   必需 (1)                    |
|                 [**IRP \_ MN \_ 写入 \_ 配置**](irp-mn-write-config.md)                  |0x10|                     否                      |                      否                      |                   必需 (1)                    |
|                 [**IRP \_ MN \_ 弹出**](irp-mn-eject.md)                  |0x11|                     否                      |                      否                      |                   必需                   |
|                     [**IRP \_ MN \_ 设置 \_ 锁定**](irp-mn-set-lock.md)                      |0x12|                     否                      |                      否                      |                   必需 (1)                    |
|                     [**IRP \_ MN \_ 查询 \_ ID**](irp-mn-query-id.md)                      |0x13|                                             |                                              |                                                  |
|                               -   **BusQueryDeviceID**                                |x|                     否                      |                      否                      |                     必需                     |
|                              -   **BusQueryHardwareIDs**                              |x|                     否                      |                      否                      |                     可选                     |
|                             -   **BusQueryCompatibleIDs**                             |x|                     否                      |                  否  |  可选                  |                                                  |
|                              -   **BusQueryInstanceID**                               |x|                     否                      |                      否                      |                     可选                     |
|                              -   **BusQueryContainerID**                              |x|                     否                      |                      否                      |                   必需 (3)                    |
|      [**IRP \_ MN \_ 查询 \_ PNP \_ 设备 \_ 状态**](irp-mn-query-pnp-device-state.md)       |0x14|                  可选                   |                   可选                   |                     可选                     |
|        [**IRP \_ MN \_ 查询 \_ 总线 \_ 信息**](irp-mn-query-bus-information.md)        |0x15|                     否                      |                      否                      |                   必需 (1)                    |
|    [**IRP \_ MN \_ 设备 \_ 使用 \_ 通知**](irp-mn-device-usage-notification.md)    |0x16|                必需 (1)                  |                 必需 (1)                  |                   必需 (1)                    |
|             [**IRP \_ MN \_ 意外 \_ 删除**](irp-mn-surprise-removal.md)              |0x17|                  必选                   |                   必选                   |                     必选                     |
|            [**IRP \_ MN \_ 设备已 \_ 枚举**](irp-mn-device-enumerated.md)             |0x19|                     否                      |                      否                      |                   必需 (1)                    |

在某些情况下， (1) 必需或可选。 有关更多详细信息，请参阅 IRP 的参考页。

 (2) 总线筛选器驱动程序可能会处理 **BusRelations** 的查询。

Windows 7 和更高版本的 Windows 中支持 (3) 。
