---
title: Storport 驱动程序微型端口例程
description: 介绍了 Storport 微型端口驱动程序例程和 SCSI 端口驱动程序的设计和 Storport 驱动程序之间的差异。
ms.assetid: ''
keywords:
- Storport 驱动程序支持例程
- 存储 WDK
- 存储支持例程
ms.date: 06/11/2018
ms.localizationpriority: medium
ms.openlocfilehash: d2a41b99c22ddd6b189b42379926cdd58bf8416b
ms.sourcegitcommit: 132f0c2d827982b808053ecd3b4d137a2883cca1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2019
ms.locfileid: "56577636"
---
# <a name="storport-driver-miniport-routines"></a>Storport 驱动程序微型端口例程

适用于 Storport 驱动程序微型端口驱动程序必须包含在本部分中列出的常规说明实现，并且必须公开是通过[HW_INITIALIZATION_DATA](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/ns-storport-_hw_initialization_data)结构期间微型端口驱动程序的初始化阶段。

Storport 微型端口驱动程序例程位于等效于其 SCSI 端口对应项的大多数方面 (请参阅[SCSI 微型端口驱动程序例程](https://technet.microsoft.com/ff565312(v=vs.96))有关详细信息)。 但是，有重要区别 SCSI 端口驱动程序的设计和 Storport 驱动程序，并且这些例程必须适应这些区别。

例如，微型端口驱动程序，使用 Storport 驱动程序必须始终准备好接收另一 I/O 请求后[HwStorStartIo](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nc-storport-hw_startio)已完成例程。 适用于 SCSI 端口的微型端口驱动程序不需要执行此操作。 SCSI 端口版本不会接收新的 I/O 请求，直到显式发出信号端口驱动程序，使用[StorPortNotification](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportnotification)函数，它已准备好处理另一个请求。

如果 Storport 微型端口驱动程序的版本不能在提交，它具有一组的队列管理功能，到 SCSI 端口版本，不可用的时间处理请求，允许其处理的重载。 Storport 微型端口驱动程序的版本类似于 SCSI 端口版本，完成的请求**SRB_STATUS_BUSY**，但与不同的 SCSI 端口版本，它还可以将标记为忙使用设备队列[StorPortDeviceBusy](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportdevicebusy)例程。 相似的功能允许为暂停和恢复处理适配器范围的基础上的微型端口驱动程序。

Storport 驱动程序提供的支持例程的详细信息，请参阅[Storport 驱动程序支持例程](storport-driver-support-routines.md)。

Storport 驱动程序有关的详细信息，请参阅[存储端口驱动程序](storage-port-drivers.md)。

以下是微型端口驱动程序例程：

|                                                                               例程                                                                               |                                                                                                                                                              描述                                                                                                                                                              |
|---------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [HW_MESSAGE_SIGNALED_INTERRUPT_ROUTINE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nc-storport-hw_message_signaled_interrupt_routine) |                                                                                                                           **HwMSInterruptRoutine**日常消息发出信号的句柄中断 (MSI)。                                                                                                                            |
|                    [HW_ADAPTER_CONTROL](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nc-storport-hw_adapter_control)                    |                                                             微型端口驱动程序**HwStorAdapterControl**例程调用来执行同步操作，从而控制的状态或行为的适配器，如停止或重新启动电源管理的 HBA。                                                             |
|                            [HW_BUILDIO](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nc-storport-hw_buildio)                            |                                                                                          **HwStorBuildIo**例程会在将其传递给之前处理不同步访问共享的系统的数据结构 SRB **HwStorStartIo**。                                                                                          |
|                        [HW_DPC_ROUTINE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nc-storport-hw_dpc_routine)                        |                                                                                        **HwStorDpcRoutine**例程是通过延迟的过程调用 (DPC) 机制在调度 IRQL 执行延迟的例程。                                                                                         |
|                       [HW_FIND_ADAPTER](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nc-storport-hw_find_adapter)                       |                                                                       **HwStorFindAdapter**例程使用提供的配置来确定是否支持特定的 HBA，如果是，则返回有关该适配器的配置信息。                                                                       |
|                         [HW_INITIALIZE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nc-storport-hw_initialize)                         |                                                                                                            **HwStorInitialize**例程在系统重新启动后初始化微型端口驱动程序或发生电源故障。                                                                                                            |
|                          [HW_INTERRUPT](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nc-storport-hw_interrupt)                          |                                                                                                                Storport 驱动程序调用**HwStorInterrupt**例程后 HBA 生成中断请求。                                                                                                                |
|         [HW_PASSIVE_INITIALIZE_ROUTINE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nc-storport-hw_passive_initialize_routine)         |                                                                                          **HwStorPassiveInitializeRoutine**后，会调用回调例程**HwStorInitialize**例程在 passive_level 调用当前 IRQL 时。                                                                                          |
|                          [HW_RESET_BUS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nc-storport-hw_reset_bus)                          |                                                                                                                        **HwStorResetBus**端口驱动程序，以清除错误条件调用例程。                                                                                                                         |
|                            [HW_STARTIO](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nc-storport-hw_startio)                            |                                                                                                                    Storport 驱动程序调用**HwStorStartIo**例程的每个传入的 I/O 请求一次。                                                                                                                    |
|                              [HW_TIMER](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nc-storport-hw_timer)                              |                                                                      **HwStorTimer**间隔，它指定何时调用微型端口驱动程序之后调用例程**StorPortNotification**与**RequestTimerCall** *NotificationType*值。                                                                      |
|                    [HW_TRACING_ENABLED](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nc-storport-hw_tracing_enabled)                    |                                                                                                        **HwStorTracingEnabled**回调例程启用 Storport 通知微型端口，启用事件跟踪。                                                                                                         |
|                       [HW_UNIT_CONTRO](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nc-storport-hw_unit_control)                        |                                           微型端口驱动程序**HwStorUnitControl**例程调用来执行同步操作，从而控制的存储单元设备状态。 微型端口驱动程序通知以启动一个单元或句柄单元设备电源状态转换。                                            |
|                           [HW_WORKITEM](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nc-storport-hw_workitem)                           |                                                                                                                          用于处理 Storport 工作项请求的微型端口提供的回调函数。                                                                                                                           |
|             [STORPORT_TELEMETRY_EVENT](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/ns-storport-_storport_telemetry_event)              |                                                                                                                       **STORPORT_TELEMETRY_EVENT**结构描述的微型端口遥测数据有效负载。                                                                                                                       |
|                  [StorPortLogTelemetry](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportlogtelemetry)                  | **StorPortLogTelemetry**例程记录来帮助诊断或收集任何有用的信息的微型端口遥测事件。 微型端口可以记录八个常规用途名称 / 值对和最大长度为 4 KB，以及相关的多个事件的缓冲区字段的结构中定义**STORPORT_TELEMETRY_EVENT**。 |
