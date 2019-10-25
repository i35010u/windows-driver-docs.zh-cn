---
title: 使用中断来唤醒设备
description: 当设备转换为低功耗状态时，框架会断开连接（或报告为非活动）用于 i/o 处理的中断。
ms.assetid: 6A4E62BD-B10F-4F01-B4B4-1FF5086710D4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 270c36b954941d9cd518cc2d0f9cb636001fab69
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843100"
---
# <a name="using-an-interrupt-to-wake-a-device"></a>使用中断来唤醒设备


当设备转换为低功耗状态时，框架会断开连接（或报告为非活动）用于 i/o 处理的中断。 从 Windows 8.1 上运行的 KMDF 1.13 和 UMDF 2.0 开始，WDF 驱动程序可以创建一个框架中断对象，该对象在设备转换为低功率状态时保持活动状态，然后可用于唤醒设备，并将其还原到完全开机 D0 状态。

如果要为芯片（SoC）平台上的系统开发 WDF 驱动程序，可以使用此类中断来唤醒不提供传统唤醒信号机制的设备。 若要使用此功能，设备必须对唤醒中断提供硬件支持，如通过 ACPI 公开。 创建中断的驱动程序必须是设备的电源策略所有者。

当设备转换为低功耗状态时，框架不会断开已被标识为唤醒功能的中断。 当设备中断时，框架会调用驱动程序的[*EvtDeviceD0Entry*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry)和[*EvtInterruptIsr*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_isr)回调例程，以 IRQL = 被动\_级别。

如果驱动程序已为 i/o 处理创建了[被动级别中断对象](supporting-passive-level-interrupts.md)，我们建议为唤醒功能共享该相同的中断对象。 在此方案中，驱动程序的[*EvtInterruptIsr*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_isr)回调例程实现条件逻辑，以便对与 i/o 相关的中断执行处理，并实现唤醒处理。

但是，如果驱动程序使用的中断需要在设备的 IRQL （DIRQL）上进行处理，则建议创建其他框架中断对象来提供唤醒功能。

按照以下步骤在 KMDF 或 UMDF 驱动程序中创建支持唤醒的中断对象：

1.  从[*EvtDriverDeviceAdd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)调用[**WdfDeviceAssignS0IdleSettings**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceassigns0idlesettings)，在*IdleCaps*参数中指定**IdleCanWakeFromS0** 。
2.  也可以调用[**WdfDeviceInitSetPowerPolicyEventCallbacks**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetpowerpolicyeventcallbacks)来注册[支持系统唤醒](supporting-system-wake-up.md)中所述的事件回调函数。
3.  调用[**wdf\_中断\_config\_INIT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nf-wdfinterrupt-wdf_interrupt_config_init)初始化[**wdf\_中断\_配置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/ns-wdfinterrupt-_wdf_interrupt_config)结构。 提供要在被动级别调用的[*EvtInterruptIsr*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_isr)回调函数。 在配置结构中，将**PassiveHandling**和**CanWakeDevice**设置为**TRUE**。 然后从驱动程序的[*EvtDevicePrepareHardware*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)回调函数调用[**WdfInterruptCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nf-wdfinterrupt-wdfinterruptcreate) ，以创建框架中断对象。
4.  调用[**WdfDeviceAssignSxWakeSettings**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceassignsxwakesettings)以将设备配置为从低功耗状态唤醒系统。
    ```cpp
    WDF_DEVICE_POWER_POLICY_WAKE_SETTINGS_INIT(&wakeSettings);
    wakeSettings.DxState = PowerDeviceD3;
    wakeSettings.UserControlOfWakeSettings = WakeDoNotAllowUserControl;
    wakeSettings.Enabled = WdfTrue;

    status = WdfDeviceAssignSxWakeSettings(Device, &wakeSettings);
    if (!NT_SUCCESS(status)) {
        Trace(TRACE_LEVEL_ERROR,"WdfDeviceAssignSxWakeSettings failed %x\n", status);
        return status;
    }
    ```

5.  当设备转换为低功耗状态时，框架不会为支持唤醒的中断调用[*EvtInterruptDisable*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_disable) 。 如果驱动程序提供了[*EvtDeviceArmWakeFromS0*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_arm_wake_from_s0) ，框架将调用它。
6.  当设备发出信号表示唤醒中断时，框架会调用驱动程序的[*EvtDeviceD0Entry*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry)回调例程。
7.  如果驱动程序的[*EvtDeviceD0Entry*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry)回调返回成功，则框架将在被动级别调用驱动程序的[*EvtInterruptIsr*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_isr)回调。 中断处理程序返回之前，必须在中断控制器中使中断静音。 如果驱动程序从*EvtDeviceD0Entry*返回失败代码，则框架会断开中断，并调用驱动程序的[*EvtInterruptDisable*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_disable)回调（如果驱动程序提供了此项）。
8.  如果驱动程序提供了以下唤醒事件回调例程，则框架将调用这些例程：
    -   [*EvtDeviceDisarmWakeFromS0*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_disarm_wake_from_s0)
    -   [*EvtDeviceDisarmWakeFromSx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_disarm_wake_from_sx)
    -   [*EvtDeviceWakeFromS0Triggered*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_wake_from_s0_triggered)
    -   [*EvtDeviceWakeFromSxTriggered*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_wake_from_sx_triggered)

9.  框架以正常的开机回拨顺序继续进行，如[函数或筛选器驱动程序的开机序列](power-up-sequence-for-a-function-or-filter-driver.md)中所述。

您可以使用[ **！ wdfkd**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfinterrupt)调试程序扩展显示特定中断是否已配置为支持唤醒。

唤醒中断功能不能与 USB 选择性挂起一起使用。

 

 





