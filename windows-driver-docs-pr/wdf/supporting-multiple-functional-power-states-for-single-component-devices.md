---
title: Single-Component 设备，一种或多种功能电源状态
description: 描述如何为 KMDF 驱动程序中的单组件设备实现 Fx 状态支持。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7989e0ead984a35401ea34533c33eee9117f399c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96815581"
---
# <a name="supporting-single-component-devices-with-single-or-multiple-functional-power-states"></a>支持单组件设备呈现单个或多个功能性电源状态


单组件设备的 KMDF 驱动程序可以定义组件的一个或多个功能电源状态，并注册回调函数，当组件的 Fx 状态发生更改时，或其活动/空闲状态发生更改时，电源管理框架 (PoFx) 调用此功能。 从 UMDF 版本2.0 开始，单组件设备的 UMDF 驱动程序可以定义单一功能电源状态 (F0) 。

有关 PoFx 的详细信息，请参阅 [电源管理框架概述](../kernel/overview-of-the-power-management-framework.md)。

若要为单组件设备实现 Fx 状态支持，必须在设备首次启动之前或期间按顺序执行以下操作。

1.  此步骤仅适用于 KMDF 驱动程序。 调用 [**WdfDeviceWdmAssignPowerFrameworkSettings**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicewdmassignpowerframeworksettings) 可指定 WDF 在向 PoFx 注册时使用的 power framework 设置。 在该驱动程序调用 **WdfDeviceWdmAssignPowerFrameworkSettings** 时提供的 [**WDF \_ POWER \_ FRAMEWORK \_ 设置**](/windows-hardware/drivers/ddi/wdfdevice/ns-wdfdevice-_wdf_power_framework_settings)结构中，驱动程序可以提供指向多个回调函数的指针。 如果驱动程序仅支持单一功能电源状态 (F0) ，则此步骤是可选的。
2.  此步骤适用于 KMDF 驱动程序和 UMDF 驱动程序。 调用 [**WdfDeviceAssignS0IdleSettings**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceassigns0idlesettings) ，并将 [**WDF \_ 设备 \_ 电源 \_ 策略 \_ 空闲 \_ 设置**](/windows-hardware/drivers/ddi/wdfdevice/ns-wdfdevice-_wdf_device_power_policy_idle_settings)结构的 **IdleTimeoutType** 字段设置为 **SystemManagedIdleTimeout** 或 **SystemManagedIdleTimeoutWithHint**。 这样做会导致 WDF 注册到 PoFx。

    对于 KMDF 驱动程序，当使用 PoFx 注册时，框架将使用该驱动程序在其调用 [**WdfDeviceWdmAssignPowerFrameworkSettings**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicewdmassignpowerframeworksettings)时在 [**WDF \_ POWER \_ framework \_ 设置**](/windows-hardware/drivers/ddi/wdfdevice/ns-wdfdevice-_wdf_power_framework_settings)中提供的信息。

由于一个设备可以多次启动（例如，在资源重新平衡的情况下），因此，驱动程序可能会在 [*EvtDeviceSelfManagedIoInit*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_init) 回调函数中执行前面的步骤。 如果驱动程序注册了一个 *EvtDeviceSelfManagedIoInit* 回调函数，则框架将在第一次调用该驱动程序的 [*EvtDeviceD0Entry*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry) 回调函数后，为每个设备调用一次此函数。

本主题中的其余信息仅适用于 KMDF 驱动程序。

## <a name="powering-up"></a>通电


当驱动程序调用 [**WdfDeviceWdmAssignPowerFrameworkSettings**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicewdmassignpowerframeworksettings)时，它可以提供指向 [*EvtDeviceWdmPostPoFxRegisterDevice*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_post_po_fx_register_device) 回调函数的指针。

框架向 PoFx 注册后，框架将调用驱动程序的 [*EvtDeviceWdmPostPoFxRegisterDevice*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_post_po_fx_register_device) 回调函数。 下面是典型的开机序列示例：

1.  [*EvtDevicePrepareHardware*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)
2.  [*EvtDeviceD0Entry*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry) (*PrevState*  =  **WdfPowerDeviceD3Final**) 
3.  [*EvtInterruptEnable*](/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_enable)
4.  [*EvtDeviceWdmPostPoFxRegisterDevice*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_post_po_fx_register_device) //PoFx 句柄可用

如果该驱动程序必须使用 POHANDLE for power framework 注册来执行任何其他操作，则该驱动程序将提供 [*EvtDeviceWdmPostPoFxRegisterDevice*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_post_po_fx_register_device) 回调。 例如，它可以指定延迟、常驻和唤醒要求。 有关使用 POHANDLE 的例程的详细信息，请参阅 [设备电源管理例程](/windows-hardware/drivers/ddi/index)。

你的驱动程序还可以使用 POHANDLE 通过 PoFx 交换电源控制请求：

-   若要将 power control 请求发送到 PoFx，驱动程序提供了 [*EvtDeviceWdmPostPoFxRegisterDevice*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_post_po_fx_register_device) 回调函数，然后使用生成的 POHANDLE 调用 [**PoFxPowerControl**](/windows-hardware/drivers/ddi/wdm/nf-wdm-pofxpowercontrol)。
-   若要执行 PoFx 请求的电源控制操作，驱动程序会在其 [**WDF \_ power \_ FRAMEWORK \_ 设置**](/windows-hardware/drivers/ddi/wdfdevice/ns-wdfdevice-_wdf_power_framework_settings)结构中提供 [*PowerControlCallback*](/windows-hardware/drivers/ddi/wdm/nc-wdm-po_fx_power_control_callback)回调例程。

## <a name="powering-down"></a>关机


WDF 在删除使用 PoFx 的指定注册之前调用 [*EvtDeviceWdmPrePoFxUnregisterDevice*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_pre_po_fx_unregister_device) 回调函数。

驱动程序可以在提供给 [**WdfDeviceWdmAssignPowerFrameworkSettings**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicewdmassignpowerframeworksettings)的 [**WDF \_ POWER \_ FRAMEWORK \_ 设置**](/windows-hardware/drivers/ddi/wdfdevice/ns-wdfdevice-_wdf_power_framework_settings)结构中提供指向 [*ComponentIdleStateCallback*](/windows-hardware/drivers/ddi/wdm/nc-wdm-po_fx_component_idle_state_callback)例程的指针。 PoFx 调用此例程，通知驱动程序对指定组件的 Fx 电源状态的挂起更改。 在此回调例程中，驱动程序可以执行与功能状态更改相关的特定于硬件的操作。

例如，在将组件转换为低功率 Fx 状态之前，驱动程序可能会保存硬件状态并禁用中断和 DMA。 驱动程序调用 [**WdfInterruptReportInactive**](/windows-hardware/drivers/ddi/wdfinterrupt/nf-wdfinterrupt-wdfinterruptreportinactive) 来通知系统中断不再处于活动状态。 关闭 F 状态转换期间的中断可能会降低整体系统能耗。

驱动程序还可以提供指向其 [**WDF \_ POWER \_ FRAMEWORK \_ 设置**](/windows-hardware/drivers/ddi/wdfdevice/ns-wdfdevice-_wdf_power_framework_settings)结构中的 [*ComponentIdleConditionCallback*](/windows-hardware/drivers/ddi/wdm/nc-wdm-po_fx_component_idle_condition_callback)例程的指针。 PoFx 调用此例程通知驱动程序组件已进入空闲状态。 在这种情况下，驱动程序将开始停止其电源管理的队列和自我托管 i/o 操作的过程：

1.  对于每个设备的电源管理队列，请调用 [**WdfIoQueueStop**](/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuestop) 一次。 在每次调用 **WdfIoQueueStop** 时，提供 [*EvtIoQueueState*](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_state) 回调。 通常，驱动程序从 [*ComponentIdleConditionCallback*](/windows-hardware/drivers/ddi/wdm/nc-wdm-po_fx_component_idle_condition_callback)内调用 **WdfIoQueueStop** 。
2.  请确保快速完成从每个电源管理队列调度到驱动程序的请求。 根据具体的驱动程序，这可能涉及以下部分或全部内容：
    -   如果驱动程序没有长时间持有请求，并且未将请求转发到执行此操作的 i/o 目标，则继续执行第3步。
    -   如果驱动程序长时间持有某些请求，请将这些请求重新排队到手动队列。 然后，驱动程序可以在 [*ComponentActiveConditionCallback*](/windows-hardware/drivers/ddi/wdm/nc-wdm-po_fx_component_active_condition_callback) 例程中检索请求。
    -   如果驱动程序将某些请求转发到长时间容纳这些请求的 i/o 目标，则取消这些请求。 在 [*ComponentActiveConditionCallback*](/windows-hardware/drivers/ddi/wdm/nc-wdm-po_fx_component_active_condition_callback)中重新提交请求。

3.  每个队列停止后，框架将调用 [*EvtIoQueueState*](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_state)。 如果驱动程序正在停止多个电源管理队列，则框架将多次调用 *EvtIoQueueState* ，每个队列一次。

    在调用最后一个 [*EvtIoQueueState*](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_state)函数之后，驱动程序必须调用 [**PoFxCompleteIdleCondition**](/windows-hardware/drivers/ddi/wdm/nf-wdm-pofxcompleteidlecondition) 。 例如，驱动程序可以在最后一个 *EvtIoQueueState* 中执行此调用。

    为了确定最后的调用，驱动程序可能会使用计数器来跟踪框架调用 [*EvtIoQueueState*](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_state)的次数。 Singlecomp 示例演示了此方法。 此示例从 Windows 8 WDK 开始提供。

下面是典型断电顺序的示例：

1.  [*ComponentIdleConditionCallback*](/windows-hardware/drivers/ddi/wdm/nc-wdm-po_fx_component_idle_condition_callback)
2.  [*ComponentIdleStateCallback*](/windows-hardware/drivers/ddi/wdm/nc-wdm-po_fx_component_idle_state_callback)
3.  [*EvtInterruptDisable*](/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_disable)
4.  [*EvtDeviceD0Exit*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_exit)

在 [*ComponentActiveConditionCallback*](/windows-hardware/drivers/ddi/wdm/nc-wdm-po_fx_component_active_condition_callback)中重新启动电源管理的队列和自行管理的 i/o 操作。

如果驱动程序之前调用 [**WdfInterruptReportInactive**](/windows-hardware/drivers/ddi/wdfinterrupt/nf-wdfinterrupt-wdfinterruptreportinactive)，请通过从 [*ComponentActiveConditionCallback*](/windows-hardware/drivers/ddi/wdm/nc-wdm-po_fx_component_active_condition_callback)或 [*ComponentIdleStateCallback*](/windows-hardware/drivers/ddi/wdm/nc-wdm-po_fx_component_idle_state_callback)调用 [**WdfInterruptReportActive**](/windows-hardware/drivers/ddi/wdfinterrupt/nf-wdfinterrupt-wdfinterruptreportactive)来重新启用非活动中断。

 

