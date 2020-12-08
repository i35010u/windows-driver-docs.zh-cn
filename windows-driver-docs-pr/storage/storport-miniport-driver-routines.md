---
title: Storport 驱动程序微型端口例程
description: 介绍了 Storport 微型端口驱动程序例程，以及 SCSI 端口驱动程序的设计和 Storport 驱动程序的设计之间的差异。
keywords:
- Storport 驱动程序支持例程
- 存储 WDK
- 存储支持例程
ms.date: 10/08/2019
ms.localizationpriority: medium
ms.openlocfilehash: c58782c7789e28de6d9bd34539bbadaeb1a3e614
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96820505"
---
# <a name="storport-driver-miniport-routines"></a>Storport 驱动程序微型端口例程

与 Storport 驱动程序配合使用的微型端口驱动程序必须包含本部分中列出的例程说明的实现，并且它必须在微型端口驱动程序的初始化阶段通过 [HW_INITIALIZATION_DATA](/windows-hardware/drivers/ddi/storport/ns-storport-_hw_initialization_data-r1) 结构公开它们。

Storport 微型端口驱动程序例程在大多数方面都等效于其 SCSI 端口对应项 (参阅 [Scsi 微型端口驱动程序例程](scsi-miniport-driver-routines.md)) 的详细信息。 但是，SCSI 端口驱动程序的设计和 Storport 驱动程序的设计之间存在重要差异，并且这些例程必须适应这些差异。

例如，使用 Storport 驱动程序的微型端口驱动程序必须始终准备好在 [HwStorStartIo](/windows-hardware/drivers/ddi/storport/nc-storport-hw_startio) 例程完成后接收另一个 i/o 请求。 使用 SCSI 端口的微型端口驱动程序无需执行此操作。 SCSI 端口版本不会接收到新的 i/o 请求，直到使用 [StorPortNotification](/windows-hardware/drivers/ddi/storport/nf-storport-storportnotification) 函数显式发出端口驱动程序的信号，然后才能处理另一请求。

如果小型端口驱动程序的 Storport 版本无法在提交请求时处理请求，则它将具有一组队列管理功能，而不能用于 SCSI 端口版本，使其能够处理重载。 与 SCSI 端口版本一样，微型端口驱动程序的 Storport 版本完成了 **SRB_STATUS_BUSY** 的请求，但与 scsi 端口版本不同的是，它还可以使用 [StorPortDeviceBusy](/windows-hardware/drivers/ddi/storport/nf-storport-storportdevicebusy) 例程将设备队列标记为忙。 类似的功能允许微型端口驱动程序在适配器范围内暂停和恢复处理。

有关 Storport 驱动程序提供的支持例程的详细信息，请参阅 [storport 驱动程序支持例程](storport-driver-support-routines.md)。

有关 Storport 驱动程序的详细信息，请参阅 [存储端口驱动程序](storage-port-drivers.md)。

下面是微型端口驱动程序例程：

| 例程所返回的值 | 描述 |
| ------- | ----------- |
| [HW_MESSAGE_SIGNALED_INTERRUPT_ROUTINE](/windows-hardware/drivers/ddi/storport/nc-storport-hw_message_signaled_interrupt_routine) | 处理 (MSI) 的消息信号中断。 |
| [HW_ADAPTER_CONTROL](/windows-hardware/drivers/ddi/storport/nc-storport-hw_adapter_control) | 执行同步操作以控制适配器的状态或行为，如停止或重启 HBA 以进行电源管理。 |
| [HW_BUILDIO](/windows-hardware/drivers/ddi/storport/nc-storport-hw_buildio) | 在将共享系统数据结构传递到 **HwStorStartIo** 之前，处理对该 SRB 的不同步访问。 |
| [HW_DPC_ROUTINE](/windows-hardware/drivers/ddi/storport/nc-storport-hw_dpc_routine) | 通过延迟的过程调用 (DPC) 机制，通过延迟的过程调用，延迟在调度 IRQL 处执行。 |
| [HW_FIND_ADAPTER](/windows-hardware/drivers/ddi/storport/nc-storport-hw_find_adapter) | 使用提供的配置来确定是否支持特定的 HBA，如果是，则返回有关该适配器的配置信息。 |
| [HW_INITIALIZE](/windows-hardware/drivers/ddi/storport/nc-storport-hw_initialize) | 在系统重新启动或出现电源故障后初始化微型端口驱动程序。 |
| [HW_INTERRUPT](/windows-hardware/drivers/ddi/storport/nc-storport-hw_interrupt) | Storport 驱动程序在 HBA 生成中断请求后调用 **HwStorInterrupt** 例程。 |
| [HW_PASSIVE_INITIALIZE_ROUTINE](/windows-hardware/drivers/ddi/storport/nc-storport-hw_passive_initialize_routine) | 当当前 IRQL 处于 PASSIVE_LEVEL 时，在 **HwStorInitialize** 例程后调用。 |
| [HW_RESET_BUS](/windows-hardware/drivers/ddi/storport/nc-storport-hw_reset_bus) | 由端口驱动程序调用以清除错误条件。 |
| [HW_STARTIO](/windows-hardware/drivers/ddi/storport/nc-storport-hw_startio) | Storport 驱动程序针对每个传入 i/o 请求调用 **HwStorStartIo** 例程一次。 |
| [HW_TIMER](/windows-hardware/drivers/ddi/storport/nc-storport-hw_timer) | 在微型端口驱动程序调用 **StorPortNotification** 且 **RequestTimerCall** *NotificationType* 值指定的时间间隔后调用。 |
| [HW_TRACING_ENABLED](/windows-hardware/drivers/ddi/storport/nc-storport-hw_tracing_enabled) | 允许 Storport 通知小型端口启用了事件跟踪。 |
| [HW_UNIT_CONTROL](/windows-hardware/drivers/ddi/storport/nc-storport-hw_unit_control) | 调用以执行同步操作，以控制存储单元设备的状态。 将通知微型端口驱动程序启动单位或处理设备设备的电源状态转换。 |
| [HW_WORKITEM](/windows-hardware/drivers/ddi/storport/nc-storport-hw_workitem) | 用于处理 Storport 工作项请求的微型端口提供的回调函数。 |
| [STORPORT_TELEMETRY_EVENT](/windows-hardware/drivers/ddi/storport/ns-storport-_storport_telemetry_event) | 介绍微型端口遥测数据负载。 |
| [StorPortLogTelemetry](/windows-hardware/drivers/ddi/storport/nf-storport-storportlogtelemetry) | 记录微型端口遥测事件以帮助诊断或收集任何有用的信息。 小型端口可以记录8个常规用途名称-值对和最大长度为4KB 的缓冲区，以及结构 STORPORT_TELEMETRY_EVENT 中定义的多个事件相关字段。 |
