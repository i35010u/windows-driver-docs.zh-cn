---
title: 串行总线驱动程序层
description: 串行总线驱动程序基于由 ACPI 创建的 PDO 进行加载，并可查询和访问系统资源，如 GPIO 和 I2C 控制器执行信号控制。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b43bcf3dc5fdeb88ec5291522cc9acb59ef60b90
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96798527"
---
# <a name="serial-bus-driver-layer"></a>串行总线驱动程序层


串行总线驱动程序基于由 ACPI 创建的 PDO 进行加载，并可查询和访问系统资源，如 GPIO 和 I2C 控制器执行信号控制。

## <a name="span-idsample_mechanism_for_power_controlspanspan-idsample_mechanism_for_power_controlspanspan-idsample_mechanism_for_power_controlspansample-mechanism-for-power-control"></a><span id="Sample_Mechanism_for_Power_Control"></span><span id="sample_mechanism_for_power_control"></span><span id="SAMPLE_MECHANISM_FOR_POWER_CONTROL"></span>电源控制的示例机制


USB over USB 提供内置机制，用于 inband 信号支持睡眠 (例如，USB 选择性挂起) 和唤醒。 但是，在 SoC 平台中，支持电源控制的机制可以使用各种控制器更灵活 (和自定义) 。

下面是实现了空闲和唤醒信号的示例实现

-   \_当蓝牙控制器需要唤醒主机以便向远程 (设备发出请求（如远程连接）时，GPIO 中断主机唤醒线路会向其发出信号，如远程连接) 
-   GPIO 信号线路 BT \_ 启用了总线驱动程序的行集，在该无线电处于活动状态时，将对其进行断言)  (内核堆栈以 D0，或在蓝牙核心堆栈检测到 D2) 的空闲 (时被取消断言。

在将驱动程序加载为定期中断和新的 GPIO 信号时，将在加载驱动程序的过程中将这两个 GPIO 行视为系统资源的形式。 系统集成商和蓝牙芯片组供应商 (IHV) 在 ACPI 表中定义其互连属性。 串行总线驱动程序可以查询和缓存这些从属控制器的连接 Id，以便打开和访问其资源。

## <a name="span-idstartup_to_enable_idle_spanspan-idstartup_to_enable_idle_spanspan-idstartup_to_enable_idle_spanstartup-to-enable-idle"></a><span id="Startup_to_Enable_Idle_"></span><span id="startup_to_enable_idle_"></span><span id="STARTUP_TO_ENABLE_IDLE_"></span>启用空闲时启动


需要串行总线驱动程序才能执行以下任务，以便在 S0 系统电源状态下支持空闲：

1.  报告 PnP 和电源管理功能;作为集成设备，子 PDO 的可移动标志应设置为 WdfFalse。
2.  报告它能够支持 (蓝牙核心驱动程序) 的功能驱动程序空闲。
3.  处理唤醒信号和唤醒信号的 arm 和 disarm。
4.  接收设备电源状态通知，并同步当前设备电源状态的 i/o 完成。

**电源管理功能**

总线驱动程序创建的子 PDO 会将电源功能设置为启用空闲状态支持，并由电源管理器进行管理，包括用于指示的设置：

-   支持 D2 设备状态的能力。
-   从 D2 进入空闲和唤醒功能的功能。
-   它将系统状态映射到设备状态，并与蓝牙核心驱动程序同步。

``` syntax
WDF_DEVICE_POWER_CAPABILITIES_INIT(&PowerCaps);
…
PowerCaps.DeviceD1 = WdfFalse;
PowerCaps.DeviceD2 = WdfTrue;
…
PowerCaps.DeviceWake = PowerDeviceD2;

PowerCaps.DeviceState[PowerSystemWorking]   = PowerDeviceD0;
PowerCaps.DeviceState[PowerSystemSleeping1] = PowerDeviceD2;
PowerCaps.DeviceState[PowerSystemSleeping2] = PowerDeviceD2;
PowerCaps.DeviceState[PowerSystemSleeping3] = PowerDeviceD2;
PowerCaps.DeviceState[PowerSystemHibernate] = PowerDeviceD2;
PowerCaps.DeviceState[PowerSystemShutdown]  = PowerDeviceD3;
..
WdfDeviceSetPowerCapabilities(ChildDevice, &PowerCaps);
```

子 PDO 会创建一个 WDF 队列，用于接收来自蓝牙核心驱动程序) 请求的 IOCTL (i/o 控制。 此类请求将在启动设备之前查询接口版本和静态功能;因此，此队列不得进行电源管理。

``` syntax
QueueConfig.PowerManaged = WdfFalse;

QueueConfig.EvtIoDeviceControl = PdoIoQuDeviceControl;

Status = WdfIoQueueCreate(ChildDevice, 
                          &QueueConfig, 
                          WDF_NO_OBJECT_ATTRIBUTES,
                          &Queue);
```

**针对空闲功能的蓝牙传输特定查询**

除了) 之前部分中突出显示的电源管理功能 (，子 PDO 还会对蓝牙核心驱动程序的查询进行响应，使其能够进入空闲状态。 为了支持 S0 中的空闲，将设置此标志：

``` syntax
FdoExtension->BthXCaps.IsDeviceIdleCapable = TRUE;
```

**用于唤醒的 Arm 和 Disarm**

空闲支持的要求是从远程蓝牙设备接收唤醒请求的功能。 此类唤醒请求的设置涉及唤醒。 蓝牙功能的 PDO 可以注册以接收回调以完成 arm/disarm 操作：

``` syntax
WDF_PDO_EVENT_CALLBACKS_INIT(&Callbacks);

// Receive this callback to arming the device for wake
Callbacks.EvtDeviceEnableWakeAtBus  = PdoDevEnableWakeAtBus;

// Receive this callback to disarming the device for wake
Callbacks.EvtDeviceDisableWakeAtBus = PdoDevDisableWakeAtBus;

WdfPdoInitSetEventCallbacks(DeviceInit, &Callbacks);
```

支持上述机制后，蓝牙核心驱动程序可以启用空闲和唤醒支持。

**设备电源状态通知**

子 PDO 注册接收进入和退出 D0 的回调，以便获得设备电源状态转换的通知。 当前设备电源状态用于同步 IO 完成–即，正常 IO 完成只能在 D0 中完成。

``` syntax
    //
    // Register to receive device power state change notification
    //
    WDF_PNPPOWER_EVENT_CALLBACKS_INIT(&PnpPowerCallbacks);  

    PnpPowerCallbacks.EvtDeviceD0Entry = PdoDevD0Entry;
    PnpPowerCallbacks.EvtDeviceD0Exit  = PdoDevD0Exit; 

    
    WdfDeviceInitSetPnpPowerEventCallbacks(DeviceInit, 
                                           &PnpPowerCallbacks);
```

## <a name="span-idarm_for_wakespanspan-idarm_for_wakespanspan-idarm_for_wakespanarm-for-wake"></a><span id="Arm_for_Wake"></span><span id="arm_for_wake"></span><span id="ARM_FOR_WAKE"></span>用于唤醒的 Arm


进入空闲状态之前，串行总线驱动程序将接收回拨 [**EvtDeviceEnableWakeAtBus**](/windows-hardware/drivers/ddi/wdfpdo/nc-wdfpdo-evt_wdf_device_enable_wake_at_bus) 到 arm 进行唤醒。

用于唤醒的机制适用于 SoC 平台特定的供应商，因此在本部分的范围之外。 但是，Windows 要求总线驱动程序准备好接收唤醒信号，并且将有一个回调函数 (例如 ISR) 来处理此类信号。

## <a name="span-identer_idlespanspan-identer_idlespanspan-identer_idlespanenter-idle"></a><span id="Enter_Idle"></span><span id="enter_idle"></span><span id="ENTER_IDLE"></span>输入空闲


蓝牙核心驱动程序启用基于时间的空闲检测机制。 满足空闲要求后，核心驱动程序开始启动堆栈以进入空闲状态。 它会调用 [**PoRequestPowerIrp**](/windows-hardware/drivers/ddi/wdm/nf-wdm-porequestpowerirp) 来设置与完成函数一起进入 D2 的能力。 在总线驱动程序完成 IRP 后，将调用此完成函数。 此时，转换到 D2 已完成。

过渡到空闲状态时，蓝牙核心驱动程序将取消所有挂起的读取请求，并在恢复到活动状态时重新启动它们。 要使串行总线驱动程序本身进入空闲状态，需要一个空的 power 托管队列。

除了空闲超时外，蓝牙核心驱动程序在进入空闲状态之前需要考虑许多不同的情况，例如：

-   等待刚发出的 HCI 命令完成。 注意：蓝牙核心驱动程序将不会进入空闲状态，直到其完成。
-   所有连接的设备都处于 "探查" 模式。

在此空闲状态下，多功能控制器可以选择通过蓝牙功能来限制其功能，但它必须继续提供电源来维护其可变的设置和配置。 然后，它可以依赖于它的唤醒机制将堆栈唤醒回活动 (D0) 状态，在这种情况之后，就可以恢复 i/o 通信。

## <a name="span-idwake_from_sleepspanspan-idwake_from_sleepspanspan-idwake_from_sleepspanwake-from-sleep"></a><span id="Wake_from_Sleep"></span><span id="wake_from_sleep"></span><span id="WAKE_FROM_SLEEP"></span>从睡眠状态唤醒


虽然蓝牙功能已与一个或多个设备配对并且处于睡眠状态，但其无线电会定期扫描其配对设备发出的请求。 当配对设备启动请求并收到蓝牙无线电时，恢复到活动状态的过程将开始。 一旦设备堆栈恢复为活动 (D0) ，驱动程序便可开始为此远程请求提供服务。

此远程请求由总线驱动程序中的唤醒信号处理函数处理，如上一部分中所述。 此唤醒信号处理函数应确保 PDO 的设备状态确实处于 D2 状态，然后调用 [**WdfDeviceIndicateWakeStatus**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceindicatewakestatus) (PDO、成功状态) 通知 KMDF 完成 W/w (等待唤醒) IRP。 此时，可以调用此 W/W IRP 的完成函数，并由其发起程序进行处理-蓝牙核心驱动程序和电源策略所有者。

完成 W/W IRP 后，将触发蓝牙核心驱动程序以启动到 D0 的转换。 它请求具有完成函数的 [**PoRequestPowerIrp**](/windows-hardware/drivers/ddi/wdm/nf-wdm-porequestpowerirp) ，以将设备电源状态设置为 D0。

在恢复到活动 D0 状态之前，串行总线驱动程序可能会收到通知 [**EvtDeviceDisableWakeAtBus**](/windows-hardware/drivers/ddi/wdfpdo/nc-wdfpdo-evt_wdf_device_disable_wake_at_bus) 以禁用唤醒功能，这就完成了对 [**EvtDeviceEnableWakeAtBus**](/windows-hardware/drivers/ddi/wdfpdo/nc-wdfpdo-evt_wdf_device_enable_wake_at_bus) 之前执行的反向操作。

蓝牙驱动程序堆栈恢复到 D0 后，串行总线驱动程序可以完成远程设备请求。

某些事件需要在串行总线驱动程序中进行同步，例如：

-   如果输入 D2，则应该已经有一个挂起的 W/W Irp。 这是在接收 W/W Irp 时，武装接收唤醒信号的唤醒信号应发生的情况。 唤醒信号仅在 D2 状态下才可操作。
-   如果在输入 D2 时数据 () 形成数据包，并且队列中没有挂起的读取请求，则总线驱动程序可以缓存传入数据并输入 D2。 然后，它可以完成 W/W Irp (，并成功) 将系统唤醒回 D0，重新挂起并完成读取请求。
-   Bthport 取消所有挂起的读取请求并等待其完成，然后再进入 D2。 同时，串行总线驱动程序可能接收到了完整的 HCI 数据包，并已取消排队以返回此 HCI 数据包。 串行总线驱动程序应完成此请求，然后将启动以输入 D2。

由主机端上的蓝牙应用程序启动的操作也可以从空闲状态唤醒堆栈。 在这种情况下，仅需要设备电源状态转换，此操作由蓝牙核心驱动程序启动。

为了缩短开机时间，回调函数 (例如，串行总线驱动程序中的 EnterD0 和唤醒) 不应标记为可分页。

## <a name="span-ida_flowchart_to_express_the__idle_wake__arm_disarm__and_device_power_state_transitionsspanspan-ida_flowchart_to_express_the__idle_wake__arm_disarm__and_device_power_state_transitionsspanspan-ida_flowchart_to_express_the__idle_wake__arm_disarm__and_device_power_state_transitionsspana-flowchart-to-express-the-idlewake-armdisarm-and-device-power-state-transitions"></a><span id="A_flowchart_to_express_the__idle_wake__arm_disarm__and_device_power_state_transitions"></span><span id="a_flowchart_to_express_the__idle_wake__arm_disarm__and_device_power_state_transitions"></span><span id="A_FLOWCHART_TO_EXPRESS_THE__IDLE_WAKE__ARM_DISARM__AND_DEVICE_POWER_STATE_TRANSITIONS"></span>用于表示空闲/唤醒、arm/disarm 和设备电源状态转换的流程图


下面是一个简化的流程图，用于说明空闲和唤醒支持的典型序列和逻辑。 此逻辑跨许多驱动程序和线程，并且有一些例外情况以及不表示 (的情况，例如，主机端上的应用程序也可以将堆栈从空闲状态唤醒) 。

![蓝牙设备电源状态转换流程图](images/bthdevicepwrstatetransitionsflowchart.png)

## <a name="span-idbus_driver_s_own_power_managementspanspan-idbus_driver_s_own_power_managementspanspan-idbus_driver_s_own_power_managementspanbus-drivers-own-power-management"></a><span id="Bus_Driver_s_own_Power_Management"></span><span id="bus_driver_s_own_power_management"></span><span id="BUS_DRIVER_S_OWN_POWER_MANAGEMENT"></span>总线驱动程序自己的电源管理


串行总线驱动程序是一种功能驱动程序 (FD) ，电源策略所有者 (其层的 PPO) 。 因此，它需要处理自己的电源管理。 在所有子节点进入较低的设备电源状态之后，它会进入较低的电源状态。 如果已准备好进入此低功耗状态，它可以取消任何挂起的对 UART 控制器驱动程序的 i/o 请求–这将允许 UART 驱动程序还进入较低的电源状态。 但是，UART 驱动程序应保留并还原其设备设置 (包括波特率) 在其电源状态之后恢复为活动状态。

 

