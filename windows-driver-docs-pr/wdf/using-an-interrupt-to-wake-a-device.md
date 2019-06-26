---
title: 使用中断来唤醒设备
description: 当设备转换到低功耗状态时，framework 断开连接 （或报告为非活动状态） 用于 I/O 的中断处理。
ms.assetid: 6A4E62BD-B10F-4F01-B4B4-1FF5086710D4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a61417355b009bbaaa875b53f06a15608819ee72
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372277"
---
# <a name="using-an-interrupt-to-wake-a-device"></a>使用中断来唤醒设备


当设备转换到低功耗状态时，framework 断开连接 （或报告为非活动状态） 用于 I/O 的中断处理。 从开始 KMDF 1.13 并且 UMDF Windows 8.1 上运行的 2.0，WDF 驱动程序可以创建一个框架中断对象的保持活动状态时设备转换为低功耗状态，并使用以唤醒设备并将其还原到其完全处于 D0 状态。

如果你正在针对系统芯片 (SoC) 平台上开发 WDF 驱动程序，可以使用此类中断以唤醒不提供传统的唤醒信号机制的设备。 若要使用此功能，设备必须具有唤醒中断的硬件支持，如通过 ACPI 公开。 创建中断的驱动程序必须是设备的电源策略所有者。

当设备转换到低功耗状态时，框架不会断开已标识为支持唤醒的中断。 设备会中断，框架将调用的驱动程序[ *EvtDeviceD0Entry* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry)并[ *EvtInterruptIsr* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_isr)在回调例程IRQL = 被动\_级别。

如果您的驱动程序已通过创建[被动级别中断对象](supporting-passive-level-interrupts.md)对于 I/O 处理，我们建议共享同一中断对象唤醒功能。 在此方案中，该驱动程序的[ *EvtInterruptIsr* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_isr)回调例程实现条件逻辑来为 O 相关中断执行处理，以及唤醒处理。

但是，如果您的驱动程序使用需要处理在设备的 IRQL (DIRQL) 中断，我们建议创建一个附加的框架中断对象来提供唤醒功能。

请按照下列步骤在 KMDF 或 UMDF 驱动程序中创建支持唤醒的中断对象：

1.  调用[ **WdfDeviceAssignS0IdleSettings**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceassigns0idlesettings)，通常是从[ *EvtDriverDeviceAdd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)，并指定**IdleCanWakeFromS0**中*IdleCaps*参数。
2.  （可选） 调用[ **WdfDeviceInitSetPowerPolicyEventCallbacks** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitsetpowerpolicyeventcallbacks)注册事件回调函数中所述[支持系统唤醒](supporting-system-wake-up.md)。
3.  调用[ **WDF\_中断\_CONFIG\_INIT** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nf-wdfinterrupt-wdf_interrupt_config_init)初始化[ **WDF\_中断\_CONFIG** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/ns-wdfinterrupt-_wdf_interrupt_config)结构。 提供[ *EvtInterruptIsr* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_isr)回调函数，以在被动级别调用。 配置结构，在设置**PassiveHandling**并**CanWakeDevice**到**TRUE**。 然后调用[ **WdfInterruptCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nf-wdfinterrupt-wdfinterruptcreate)从您的驱动程序[ *EvtDevicePrepareHardware* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)创建框架的回调函数中断对象。
4.  调用[ **WdfDeviceAssignSxWakeSettings** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceassignsxwakesettings)来配置设备以将系统从低功耗状态唤醒。
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

5.  当设备转换到低功耗状态时，该框架不会调用[ *EvtInterruptDisable* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_disable)支持唤醒的中断。 调用 framework does [ *EvtDeviceArmWakeFromS0* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_arm_wake_from_s0)如果驱动程序提供了一个。
6.  设备向发出信号唤醒中断，框架将调用的驱动程序[ *EvtDeviceD0Entry* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry)回调例程。
7.  如果驱动程序的[ *EvtDeviceD0Entry* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry)回调返回成功，则框架将调用的驱动程序[ *EvtInterruptIsr* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_isr)回调在被动级别。 中断处理程序返回之前，它必须提示中断控制器中的中断。 如果驱动程序返回了失败代码从*EvtDeviceD0Entry*，该框架断开连接中断，并调用在驱动程序[ *EvtInterruptDisable* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_disable)回调中，如果驱动程序提供了一个。
8.  如果该驱动程序已提供任何，框架将调用以下唤醒事件回调例程：
    -   [*EvtDeviceDisarmWakeFromS0*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_disarm_wake_from_s0)
    -   [*EvtDeviceDisarmWakeFromSx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_disarm_wake_from_sx)
    -   [*EvtDeviceWakeFromS0Triggered*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_wake_from_s0_triggered)
    -   [*EvtDeviceWakeFromSxTriggered*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_wake_from_sx_triggered)

9.  框架将继续与正常强化回调序列，如中所述[函数或筛选器驱动程序的启动顺序](power-up-sequence-for-a-function-or-filter-driver.md)。

可以使用[ **！ wdfkd.wdfinterrupt** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfinterrupt)调试器扩展才会显示是否已配置特定的中断，才能唤醒。

不能使用唤醒中断功能结合 USB 选择性挂起。

 

 





