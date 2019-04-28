---
title: 串行总线驱动程序层
description: 串行总线驱动程序已加载基于创建的 ACPI，PDO 和可以查询和访问系统资源，如 GPIO 和 I2C 控制器以执行信号的控件。
ms.assetid: E6A3E1CF-C25B-429B-946D-B300BAF3CF9B
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: de4b7a842b8f49498a353ffe949fd36a6d8ea264
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63328194"
---
# <a name="serial-bus-driver-layer"></a>串行总线驱动程序层


串行总线驱动程序已加载基于创建的 ACPI，PDO 和可以查询和访问系统资源，如 GPIO 和 I2C 控制器以执行信号的控件。

## <a name="span-idsamplemechanismforpowercontrolspanspan-idsamplemechanismforpowercontrolspanspan-idsamplemechanismforpowercontrolspansample-mechanism-for-power-control"></a><span id="Sample_Mechanism_for_Power_Control"></span><span id="sample_mechanism_for_power_control"></span><span id="SAMPLE_MECHANISM_FOR_POWER_CONTROL"></span>示例电源控制机制


通过 USB 蓝牙已发出信号以支持 （即 USB 选择性挂起） 的睡眠和唤醒 inband 的内置机制。 但是，在 SoC 平台中，支持电源控制的机制可以是更灵活 （和可自定义） 使用不同的控制器。

下面是一个示例实现，以遍历空闲状态并唤醒信号

-   GPIO 中断主机\_唤醒行-需要唤醒要从远程设备 （例如远程连接） 为请求提供服务的主机时发出信号的蓝牙控制器
-   GPIO 信号行 BT\_启用行-由总线驱动程序设置并添加单选处于活动状态时 （在 D0 core 堆栈） 或取消添加如果蓝牙核心驱动程序检测到 （进入到 D2） 的空闲时间。

驱动程序加载，因为正则中断和新 GPIO 信号期间，将向串行总线驱动程序报告以下两个 GPIO 行形式的系统资源。 其相互连接的属性将由系统集成商和蓝牙芯片供应商 (IHV) 定义的 ACPI 表中。 串行总线驱动程序可以查询和缓存这些依赖于控制器的连接才能够打开和访问其资源 Id。

## <a name="span-idstartuptoenableidlespanspan-idstartuptoenableidlespanspan-idstartuptoenableidlespanstartup-to-enable-idle"></a><span id="Startup_to_Enable_Idle_"></span><span id="startup_to_enable_idle_"></span><span id="STARTUP_TO_ENABLE_IDLE_"></span>为启用空闲的启动


串行总线驱动程序需要支持空闲 S0 系统电源状态下执行以下任务：

1.  报表即插即用和电源管理功能;为集成的设备，它的子级的可移动标志 PDO 应设置为 WdfFalse。
2.  报告可以支持其功能驱动程序 （蓝牙核心驱动程序） 到空闲。
3.  处理 arm 和清除唤醒，并唤醒信号。
4.  接收设备电源状态通知并与当前设备电源状态同步 I/O 完成。

**电源管理功能**

子由总线驱动程序创建的 PDO 设置电源功能以支持空闲状态，并将管理的电源管理器，包括设置，以表明如：

-   若要支持 D2 设备状态，其功能。
-   输入空闲状态，并从 D2 唤醒其功能。
-   其映射到设备的系统状态的说明，而与蓝牙核心驱动程序保持同步。

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

子 PDO 创建 WDF 队列以接收来自蓝牙核心驱动程序 IOCTL （I/O 控制） 请求。 此类请求是否来自查询界面版本和之前正在启动; 在设备的静态功能因此，此队列不能电源管理。

``` syntax
QueueConfig.PowerManaged = WdfFalse;

QueueConfig.EvtIoDeviceControl = PdoIoQuDeviceControl;

Status = WdfIoQueueCreate(ChildDevice, 
                          &QueueConfig, 
                          WDF_NO_OBJECT_ATTRIBUTES,
                          &Queue);
```

**蓝牙传输特定的查询为空闲状态的功能的**

除了报告电源管理功能 （如先前部分中，突出显示部分）、 子 PDO 也响应的功能，以进入空闲状态的蓝牙核心驱动程序的查询。 为了支持空闲 S0，在设置此标志：

``` syntax
FdoExtension->BthXCaps.IsDeviceIdleCapable = TRUE;
```

**Arm 并清除唤醒**

空闲支持的一个要求是从远程的蓝牙设备接收唤醒请求的功能。 唤醒请求安装过程都包括要了解唤醒。 蓝牙函数 PDO 可以注册以接收回调以完成清除 arm/操作：

``` syntax
WDF_PDO_EVENT_CALLBACKS_INIT(&Callbacks);

// Receive this callback to arming the device for wake
Callbacks.EvtDeviceEnableWakeAtBus  = PdoDevEnableWakeAtBus;

// Receive this callback to disarming the device for wake
Callbacks.EvtDeviceDisableWakeAtBus = PdoDevDisableWakeAtBus;

WdfPdoInitSetEventCallbacks(DeviceInit, &Callbacks);
```

支持的上述机制，蓝牙核心驱动程序然后可以启用空闲状态并唤醒支持。

**设备的电源状态更改通知**

子 PDO 注册以接收回调进入和退出 D0 以获得通知的设备电源状态转换。 当前设备电源状态用于同步 IO 完成 – 即正常 IO 完成仅都应在 D0 中完成。

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

## <a name="span-idarmforwakespanspan-idarmforwakespanspan-idarmforwakespanarm-for-wake"></a><span id="Arm_for_Wake"></span><span id="arm_for_wake"></span><span id="ARM_FOR_WAKE"></span>唤醒 arm


在进入空闲状态之前, 串行总线驱动程序将收到回调[ **EvtDeviceEnableWakeAtBus** ](https://msdn.microsoft.com/library/windows/hardware/ff540866)到 arm 唤醒。

Arm 唤醒的机制是特定于 SoC 平台供应商，因此本部分的讨论范围内。 但是，Windows 要求总线驱动程序将准备好接收唤醒信号，且将有一个回调函数 (例如 ISR) 来处理这种信号。

## <a name="span-identeridlespanspan-identeridlespanspan-identeridlespanenter-idle"></a><span id="Enter_Idle"></span><span id="enter_idle"></span><span id="ENTER_IDLE"></span>输入空闲


蓝牙核心驱动程序，基于时间的空闲检测机制。 在满足空闲的要求，核心驱动程序将开始启动进入空闲状态的堆栈。 它将调用[ **PoRequestPowerIrp** ](https://msdn.microsoft.com/library/windows/hardware/ff559734)若要设置的能力以及完成函数进入 D2。 总线驱动程序已完成 IRP 后，调用此完成函数。 在此时间是，过渡到 D2 获取已完成。

时转换为空闲状态，蓝牙核心驱动程序将取消所有挂起的读取请求，并重新启动它们恢复为活动状态时。 空 power 托管的队列需要使串行总线驱动程序本身进入空闲状态。

空闲超时，除了蓝牙核心驱动程序，将考虑很多情况下进入空闲状态，如进入前：

-   等待具有刚颁发 HCI 命令完成。 注意： 蓝牙核心驱动程序将会进入空闲状态直至其完成为止。
-   所有已连接的设备处于探查模式。

在这种空闲状态，多功能控制器有选项可减少通过蓝牙函数，它的强大功能，但它必须继续提供能够维护其易失性设置和配置。 然后，它可以依赖其唤醒机制，以返回到活动 (D0) 状态之后恢复 I/O 通信可以在堆栈中唤醒。

## <a name="span-idwakefromsleepspanspan-idwakefromsleepspanspan-idwakefromsleepspanwake-from-sleep"></a><span id="Wake_from_Sleep"></span><span id="wake_from_sleep"></span><span id="WAKE_FROM_SLEEP"></span>从睡眠状态唤醒


蓝牙函数与一个或多个设备配对并处于睡眠状态，而其单选正在定期扫描来自其配对的设备的请求。 如果配对的设备启动一个请求，获取接收的蓝牙无线开始此过程恢复为活动状态。 一旦设备堆栈已恢复为活动状态 (D0)，驱动程序才能开始处理此远程请求。

在上一部分中所述，将由总线驱动程序中的唤醒信号处理函数处理此远程请求。 此唤醒信号处理函数应确保 PDO 的设备状态确实处于 D2 状态，然后调用[ **WdfDeviceIndicateWakeStatus** ](https://msdn.microsoft.com/library/windows/hardware/ff546025) (PDO，成功状态) 以通知 KMDF 完成W/W （等待唤醒） IRP。 它是在这一次此 W/W IRP 完成函数时可调用和蓝牙核心驱动程序和电源策略所有者获取由其发起方的处理。

W/W IRP 完成触发蓝牙核心驱动程序以启动到 D0 的转换。 它会请求[ **PoRequestPowerIrp** ](https://msdn.microsoft.com/library/windows/hardware/ff559734)与完成函数来设置设备电源状态为 D0。

在恢复活动 D0 状态之前串行总线驱动程序可能会收到一条通知[ **EvtDeviceDisableWakeAtBus** ](https://msdn.microsoft.com/library/windows/hardware/ff540858)若要禁用唤醒 – 这将完成过程后，若要反转什么[ **EvtDeviceEnableWakeAtBus** ](https://msdn.microsoft.com/library/windows/hardware/ff540866)像前面。

恢复到 D0 的蓝牙驱动程序堆栈后，串行总线驱动程序然后可以完成远程设备请求。

某些事件需要同步中串行总线驱动程序，如：

-   输入 D2，时应该已经有挂起的 W/W Irp。 这是当武装唤醒接收唤醒信号时应该发生而不是接收 W/W Irp。 唤醒信号 D2 状态才可操作时。
-   如果数据的到达 （以形成一个数据包） 时进入 D2 并且队列中没有任何挂起的读取的请求，总线驱动程序可以缓存传入数据，并输入 D2。 然后，它可以完成 W/W Irp （与成功） 回 D0 re 挂起系统唤醒并完成读取的请求。
-   Bthport 取消所有挂起的读取的请求并等待其完成后再进入 D2。 同时，串行总线驱动程序可能已收到完整的 HCI 数据包和已取消排队的读取的请求返回此 HCI 数据包。 串行总线驱动程序应完成此请求，并随后将启动进入 D2。

由主机端上的蓝牙应用程序启动的操作也可以唤醒从空闲状态的堆栈。 在这种情况下，仅设备电源状态转换是必需的并通过蓝牙核心驱动程序启动此操作。

为了减少启动时间，串行总线驱动程序中的回调函数 （例如 EnterD0 和唤醒） 不应标记可分页。

## <a name="span-idaflowcharttoexpresstheidlewakearmdisarmanddevicepowerstatetransitionsspanspan-idaflowcharttoexpresstheidlewakearmdisarmanddevicepowerstatetransitionsspanspan-idaflowcharttoexpresstheidlewakearmdisarmanddevicepowerstatetransitionsspana-flowchart-to-express-the-idlewake-armdisarm-and-device-power-state-transitions"></a><span id="A_flowchart_to_express_the__idle_wake__arm_disarm__and_device_power_state_transitions"></span><span id="a_flowchart_to_express_the__idle_wake__arm_disarm__and_device_power_state_transitions"></span><span id="A_FLOWCHART_TO_EXPRESS_THE__IDLE_WAKE__ARM_DISARM__AND_DEVICE_POWER_STATE_TRANSITIONS"></span>流程图来表达的空闲/唤醒、 清除 arm/和设备的电源状态转换


下面是一个简化的流程图，说明了典型的序列和空闲并且唤醒支持此逻辑。 此逻辑横跨多个驱动程序和线程，并且有异常，以及未表示的极端情况 （例如主机端上的应用程序还可以唤醒堆栈从空闲状态）。

![蓝牙设备电源状态转换流程图](images/bthdevicepwrstatetransitionsflowchart.png)

## <a name="span-idbusdriversownpowermanagementspanspan-idbusdriversownpowermanagementspanspan-idbusdriversownpowermanagementspanbus-drivers-own-power-management"></a><span id="Bus_Driver_s_own_Power_Management"></span><span id="bus_driver_s_own_power_management"></span><span id="BUS_DRIVER_S_OWN_POWER_MANAGEMENT"></span>总线驱动程序自己的电源管理


串行总线驱动程序是层的功能驱动程序 (FD) 和它的电源策略所有者 (PPO)。 因此，它需要处理其自己的电源管理。 所有子级输入较低的设备的电源状态后，它可以然后输入进入低功耗状态本身。 输入此低功率状态准备就绪时，它可以取消任何挂起的 I/O 请求到 UART 控制器驱动程序-这将允许 UART 驱动程序，还进入低功率状态。 但是，UART 驱动程序应保持和还原 （包括波特率） 其设备设置何时更高版本其电源状态恢复为活动状态。

 

 





