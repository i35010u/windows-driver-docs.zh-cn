---
title: 单组件设备、 一个或多个功能的电源状态
description: 介绍如何在 KMDF 驱动程序中实现对单个组件设备的 Fx 状态支持。
ms.assetid: C7EFD71F-E101-4160-9703-E1DBD507698C
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a7976d6ea7f8ead2fb9570a70f2559719d165bd2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368075"
---
# <a name="supporting-single-component-devices-with-single-or-multiple-functional-power-states"></a>支持单组件设备呈现单个或多个功能性电源状态


单组件设备的 KMDF 驱动程序可以定义一个或多个组件的功能的电源状态和注册组件的 Fx 状态发生更改时，电源管理框架 (PoFx) 调用的回调函数或其活动/空闲条件更改。 从 UMDF 2.0 版开始，单组件设备的 UMDF 驱动程序可以定义单个功能电源状态 (F0)。

有关 PoFx 详细信息，请参阅[电源管理框架概述](https://docs.microsoft.com/windows-hardware/drivers/kernel/overview-of-the-power-management-framework)。

若要实现对单个组件设备的 Fx 状态支持，必须执行以下操作顺序之前或期间首次启动设备。

1.  此步骤是用于 KMDF 驱动程序。 调用[ **WdfDeviceWdmAssignPowerFrameworkSettings** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicewdmassignpowerframeworksettings)指定 WDF PoFx 与注册时使用的电源框架设置。 在中[ **WDF\_POWER\_FRAMEWORK\_设置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/ns-wdfdevice-_wdf_power_framework_settings)调用时，提供了驱动程序的结构**WdfDeviceWdmAssignPowerFrameworkSettings**，该驱动程序可以提供指向几个回调函数的指针。 如果该驱动程序支持仅的单个功能电源状态 (F0)，此步骤是可选的。
2.  此步骤适用于 KMDF 驱动程序和 UMDF 驱动程序。 调用[ **WdfDeviceAssignS0IdleSettings** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceassigns0idlesettings)并设置**IdleTimeoutType**字段[ **WDF\_设备\_POWER\_策略\_IDLE\_设置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/ns-wdfdevice-_wdf_device_power_policy_idle_settings)结构**SystemManagedIdleTimeout**或**SystemManagedIdleTimeoutWithHint**。 这样做会导致 WDF PoFx 向注册。

    有关 KMDF 驱动程序，向 PoFx 注册时，框架将使用该驱动程序中提供的信息[ **WDF\_POWER\_FRAMEWORK\_设置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/ns-wdfdevice-_wdf_power_framework_settings)时它调用[ **WdfDeviceWdmAssignPowerFrameworkSettings**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicewdmassignpowerframeworksettings)。

因为可以超过一次启动设备，例如发生时重新平衡资源，驱动程序可能执行中的上一步骤[ *EvtDeviceSelfManagedIoInit* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_init)回调函数。 如果该驱动程序已注册*EvtDeviceSelfManagedIoInit*回调函数，框架将调用它一次对于每个设备，framework 有调用驱动程序的后[ *EvtDeviceD0Entry*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry)第一次的回调函数。

本主题中的信息的其余部分仅适用于 KMDF 驱动程序。

## <a name="powering-up"></a>开机


当驱动程序调用[ **WdfDeviceWdmAssignPowerFrameworkSettings**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicewdmassignpowerframeworksettings)，它可以提供一个指向[ *EvtDeviceWdmPostPoFxRegisterDevice* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_post_po_fx_register_device)回调函数。

框架将调用的驱动程序[ *EvtDeviceWdmPostPoFxRegisterDevice* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_post_po_fx_register_device)后 PoFx 框架已注册的回调函数。 下面是典型启动序列的示例：

1.  [*EvtDevicePrepareHardware*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)
2.  [*EvtDeviceD0Entry*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry) (*PrevState* = **WdfPowerDeviceD3Final**)
3.  [*EvtInterruptEnable*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_enable)
4.  [*EvtDeviceWdmPostPoFxRegisterDevice* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_post_po_fx_register_device) / / PoFx 句柄是可用

该驱动程序提供了[ *EvtDeviceWdmPostPoFxRegisterDevice* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_post_po_fx_register_device)回调如果它必须执行 POHANDLE 用于 power framework 注册任何其他操作。 例如，它也可以指定延迟，驻留和唤醒要求。 有关使用 POHANDLE 的例程的详细信息，请参阅[设备电源管理例程](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)。

您的驱动程序还可以使用 POHANDLE 交换与 PoFx 电源控制请求：

-   若要发送到 PoFx 电源控制请求，该驱动程序提供了[ *EvtDeviceWdmPostPoFxRegisterDevice* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_post_po_fx_register_device)回调函数，然后使用生成的 POHANDLE 调用[ **PoFxPowerControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-pofxpowercontrol)。
-   若要执行所请求 PoFx 电源控制操作，该驱动程序提供了[ *PowerControlCallback* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-po_fx_power_control_callback)中的回调例程其[ **WDF\_POWER\_FRAMEWORK\_设置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/ns-wdfdevice-_wdf_power_framework_settings)结构。

## <a name="powering-down"></a>关闭


WDF 调用[ *EvtDeviceWdmPrePoFxUnregisterDevice* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_pre_po_fx_unregister_device)之前删除 PoFx 与指定的注册的回调函数。

该驱动程序可以提供一个指向[ *ComponentIdleStateCallback* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-po_fx_component_idle_state_callback)例程中[ **WDF\_POWER\_FRAMEWORK\_设置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/ns-wdfdevice-_wdf_power_framework_settings)结构，它提供对[ **WdfDeviceWdmAssignPowerFrameworkSettings**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicewdmassignpowerframeworksettings)。 PoFx 调用此例程，以通知挂起的指定组件的 Fx 电源状态更改的驱动程序。 在此回调例程，该驱动程序可以执行与正常运行状态更改相关的特定于硬件的操作。

例如，进入低功耗 Fx 状态转换组件之前, 驱动程序可能会保存硬件状态和禁用中断和 DMA。 驱动程序调用[ **WdfInterruptReportInactive** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nf-wdfinterrupt-wdfinterruptreportinactive)通知给系统中断不再处于活动状态。 在 F 状态转换期间关闭中断可能会降低整体系统电源消耗。

该驱动程序还可以提供一个指向[ *ComponentIdleConditionCallback* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-po_fx_component_idle_condition_callback)例程中其[ **WDF\_POWER\_FRAMEWORK\_设置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/ns-wdfdevice-_wdf_power_framework_settings)结构。 PoFx 调用此例程来通知该驱动程序组件已进入空闲状态。 在此例程中，该驱动程序开始停止其电源管理队列和自我管理的 I/O 操作的过程：

1.  调用[ **WdfIoQueueStop** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nf-wdfio-wdfioqueuestop)一次针对每个设备的电源管理队列。 在每次调用**WdfIoQueueStop**，提供[ *EvtIoQueueState* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_state)回调。 通常情况下，驱动程序调用**WdfIoQueueStop**内[ *ComponentIdleConditionCallback*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-po_fx_component_idle_condition_callback)。
2.  请确保将被分派给该驱动程序从每个电源管理队列的请求会快速完成。 具体取决于该驱动程序，这可能涉及的以下部分或全部：
    -   如果驱动程序不包含长一段时间的请求，并且不将它们转发到 I/O 目标这样做，则继续执行步骤 3。
    -   如果该驱动程序为某些请求长时间，将重新排队到手动队列这些请求。 在其[ *ComponentActiveConditionCallback* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-po_fx_component_active_condition_callback)例程，该驱动程序然后可以检索请求。
    -   如果该驱动程序特定将请求转发到包含长一段时间的 I/O 目标，则取消这些请求。 重新提交中的请求[ *ComponentActiveConditionCallback*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-po_fx_component_active_condition_callback)。

3.  每个队列已停止，框架将调用[ *EvtIoQueueState*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_state)。 如果该驱动程序正在停止多个电源管理的队列，框架将调用*EvtIoQueueState*多次，一次为每个队列。

    该驱动程序必须调用[ **PoFxCompleteIdleCondition** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-pofxcompleteidlecondition)后的最后一个[ *EvtIoQueueState* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_state)调用函数。 例如，驱动程序可以进行此调用在以下时间内的*EvtIoQueueState*。

    若要确定的调用是最后一个对话框，该驱动程序可能使用一个计数器来跟踪的框架已调用的次数[ *EvtIoQueueState*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_state)。 Singlecomp 示例演示此方法。 此示例是在 Windows 8 WDK 中的开始提供。

下面是典型关机序列的示例：

1.  [*ComponentIdleConditionCallback*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-po_fx_component_idle_condition_callback)
2.  [*ComponentIdleStateCallback*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-po_fx_component_idle_state_callback)
3.  [*EvtInterruptDisable*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_disable)
4.  [*EvtDeviceD0Exit*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_exit)

电源管理队列和中的自托管的 I/O 操作重启[ *ComponentActiveConditionCallback*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-po_fx_component_active_condition_callback)。

如果该驱动程序之前调用[ **WdfInterruptReportInactive**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nf-wdfinterrupt-wdfinterruptreportinactive)，通过调用重新启用非活动中断[ **WdfInterruptReportActive** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nf-wdfinterrupt-wdfinterruptreportactive)眖[ *ComponentActiveConditionCallback* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-po_fx_component_active_condition_callback)或[ *ComponentIdleStateCallback*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-po_fx_component_idle_state_callback)。

 

 





