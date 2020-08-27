---
description: 本主题介绍了 UMDF 函数驱动程序如何支持 USB 选择性挂起。
title: USB UMDF 驱动程序中的选择性挂起
ms.date: 05/09/2018
ms.localizationpriority: medium
ms.openlocfilehash: 7269b9aff128a60c2f730eb410702ac7a83df68b
ms.sourcegitcommit: 15caaf6d943135efcaf9975927ff3933957acd5d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88969570"
---
# <a name="selective-suspend-in-usb-umdf-drivers"></a>USB UMDF 驱动程序中的选择性挂起


**重要的 API**

-   [**IWDFUsbTargetDevice::SetPowerPolicy**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbtargetdevice-setpowerpolicy)
-   [**IWDFDevice2::AssignSxWakeSettings**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice2-assignsxwakesettings)
-   [**IWDFDevice2::AssignS0IdleSettings**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice2-assigns0idlesettings)

本主题介绍了 UMDF 函数驱动程序如何支持 USB 选择性挂起。

UMDF 函数驱动程序可以通过以下两种方式之一来支持 USB 选择性挂起：

-   声明电源策略所有权，并处理设备空闲关机和恢复。
-   依靠 Microsoft 提供的用于处理选择性挂起的 WinUSB.sys 驱动程序。 安装 UMDF USB 驱动程序的过程中，会将 WinUSB.sys 作为内核模式设备堆栈的一部分进行安装。 WinUSB.sys 实现用于暂停和恢复 USB 设备操作的底层机制。

这两种方法只需要少量代码。 WDK 中提供的 IdleWake 示例演示了如何在 UMDF USB 驱动程序中支持选择性挂起。 可在% WinDDK% \\ BuildNumber \\ Src \\ Usb \\ OsrUsbFx2 \\ UMDF \\ Fx2 \_ Driver \\ IdleWake 中找到此示例。 此文件夹包含该示例的 PPO 和非 PPO 版本。

支持选择性挂起的 UMDF 驱动程序必须遵循以下准则：

-   UMDF 驱动程序可以为其设备堆栈声明电源策略所有权，但这不是必需的。 默认情况下，基础 WinUSB.sys 驱动程序拥有电源策略。
-   支持选择性挂起并且是 PPO 的 UMDF 驱动程序可以使用不受电源管理的电源管理的队列或队列。 支持选择性挂起但不是 PPO 的 UMDF 驱动程序不得使用电源管理的队列。

## <a name="power-policy-ownership-in-umdf-usb-drivers"></a>UMDF USB 驱动程序中的电源策略所有权


默认情况下，WinUSB.sys 是包含 UMDF USB 驱动程序的设备堆栈的 PPO。 从 WDF 1.9 开始，基于 UMDF 的 USB 驱动程序可以声明电源策略所有权。 由于每个设备堆栈中只有一个驱动程序可以是 PPO，因此 PPO 的 UMDF USB 驱动程序必须显式禁用 WinUSB.sys 中的电源策略所有权。

**在 UMDF USB 驱动程序中声明电源策略所有权**

1.  调用 **IWDFDeviceInitialize：： SetPowerPolicyOwnership** 并将 **其**传递给 TRUE，通常来自驱动程序回调对象上的 **IDriverEntry：： OnDeviceAdd** 方法。 例如：

    ``` syntax
    FxDeviceInit->SetPowerPolicyOwnership(TRUE);
    ```

2.  禁用 WinUSB 中的电源策略所有权。 在驱动程序的 INF 文件中，包括将注册表中的**WinUsbPowerPolicyOwnershipDisabled**值设置为非零值的**AddReg**指令。 **AddReg**指令必须出现在 DDInstall 部分中。 例如：

    ``` syntax
    [MyDriver_Install.NT.hw]
    AddReg=MyDriver_AddReg

    [MyDriver_AddReg]
    HKR,,"WinUsbPowerPolicyOwnershipDisabled",0x00010001,1
    ```

支持选择性挂起并由低于1.9 的 WDF 版本生成的 UMDF USB 驱动程序不得声明电源策略所有权。 在这些早期版本的 WDF 中，仅当 WinUSB.sys 是 PPO 时，USB 选择性挂起才能正常工作。

## <a name="io-queues-in-umdf-usb-drivers"></a>UMDF USB 驱动程序中的 i/o 队列


对于支持选择性挂起的 UMDF 驱动程序，UMDF 驱动程序是否拥有其设备的电源策略确定它可以使用的 i/o 队列的类型。 支持选择性挂起和 PPOs 的 UMDF 驱动程序可以使用电源管理的队列，也可以不使用电源管理的队列。 支持选择性挂起但不是 PPO 的 UMDF USB 驱动程序不应使用任何电源管理 i/o 队列。

如果设备处于挂起状态时，如果 i/o 请求到达电源管理的队列，则该框架将不会显示该请求，除非驱动程序是 PPO 的，如 [USB 驱动程序中选择性挂起](https://docs.microsoft.com/windows-hardware/drivers/usbcon/)的图像中所示。 如果 UMDF 驱动程序不是设备的 PPO，框架将无法代表设备打开设备。 因此，请求将保留在电源管理的队列中。 请求从不会达到 WinUSB，因此 WinUSB 无法启动设备。 因此，设备堆栈可以停止。

如果队列不是电源管理的，则即使关闭设备电源，框架也会向 UMDF 驱动程序提供 i/o 请求。 UMDF 驱动程序格式化请求，并以常规方式将其按设备堆栈向下转发到默认 i/o 目标。 不需要特殊代码。 当请求到达 PPO ( # A0) 时，WinUSB.sys 将对设备进行开机并执行所需的 i/o 操作。

**% WinDDK% \\ BuildNumber \\ Src \\ Usb \\ OsrUsbFx2 \\ umdf \\ Fx2 \_ driver \\ IdleWake**中的示例驱动程序定义 \_ \_ \_ \_ \_ 构建驱动程序的非 PPO 版本时，不会有固定电源策略所有者。 当驱动程序为读和写请求创建队列时，它将确定是否通过检查常量来创建一个电源管理的队列。

若要创建队列，驱动程序将调用驱动程序定义的 **CMyQueue：： Initialize** 方法，该方法采用以下三个参数：

-   *DispatchType*，一个 WDF \_ IO \_ 队列 \_ 调度 \_ 类型枚举值，指示队列调度请求的方式。
-   *默认*值，指示队列是否为默认队列的布尔值。
-   *PowerManaged*，指示队列是否为电源管理的布尔值。

下面的代码段显示了驱动程序对 **CMyQueue：： Initialize** 方法的调用，作为读写队列创建的一部分：

```cpp
#if defined(_NOT_POWER_POLICY_OWNER_)
    powerManaged = false;
#else
    powerManaged = true;
#endif  
hr = __super::Initialize(WdfIoQueueDispatchParallel,
                         true,
                         powerManaged,
                         );
```

**CMyQueue：： Initialize** ，然后调用 [**IWDFDevice：： CreateIoQueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice-createioqueue) 来创建队列，如下所示：

```cpp
hr = m_FxDevice->CreateIoQueue(
                               callback,
                               Default,
                               DispatchType,
                               PowerManaged,
                               FALSE,
                               &fxQueue
                               );
```

此代码序列会生成一个默认队列，该队列将并行发送请求。 如果驱动程序是 PPO，则队列由电源管理，如果驱动程序不是 PPO，则不会对队列进行电源管理。

## <a name="supporting-usb-selective-suspend-in-a-umdf-ppo"></a>支持在 UMDF PPO 中使用 USB 选择性挂起


为支持选择性挂起，作为其设备堆栈的 PPO 的 UMDF USB 驱动程序必须执行以下操作：

1.  如前文所述，声明设备堆栈的电源策略所有权，通常在其驱动程序回调对象上的 [**IDriverEntry：： OnDeviceAdd**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-idriverentry-ondeviceadd) 方法中。
2.  通过对框架设备对象调用 [**IWDFDevice2：： AssignS0IdleSettings**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice2-assigns0idlesettings) 方法启用选择性挂起。

**若要从 PPO 启用 USB 选择性挂起**

-   调用 [**IWDFDevice2：： AssignS0IdleSettings**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice2-assigns0idlesettings)，通常来自设备回调对象上的 **OnPrepareHardware** 方法。 将参数设置为 AssignS0IdleSettings，如下所示：
    -   *IdleCaps* 到 **IdleUsbSelectiveSuspend**。
    -   *DxState* 到框架将空闲设备转换到的设备睡眠状态。 对于 USB 选择性挂起，请指定 **PowerDeviceMaximum**，它指示框架应使用指定的总线驱动程序值。
    -   在框架将其转换为*DxState*之前，设备必须处于空闲状态的时间 *（以毫秒*为单位）。
    -   如果你的驱动程序允许用户管理空闲设置，则为*UserControlOfIdleSettings* **IdleAllowUserControl** ; 否则为**IdleDoNotAllowUserControl**。
    -   默认情况下，*启用* **WdfUseDefault**以启用选择性挂起，但允许用户的设置重写默认值。

下面的示例演示 IdleWake \_ PPO 驱动程序如何在其内部的 CMyDevice：： SetPowerManagement 方法中调用此方法：

```cpp
hr = m_FxDevice->AssignS0IdleSettings( IdleUsbSelectiveSuspend,
                                PowerDeviceMaximum,
                                IDLE_TIMEOUT_IN_MSEC,
                                IdleAllowUserControl,
                                WdfUseDefault);                                                                                                   
```

如果设备硬件可以生成唤醒信号，则 UMDF 驱动程序还可以支持从 S1、S2 或 S3 唤醒系统。 有关详细信息，请参阅 [在 UMDF 驱动程序中唤醒系统](#system-wake-in-a-umdf-driver)。

## <a name="supporting-usb-selective-suspend-in-a-non-ppo-umdf-driver"></a>在非 PPO 的 UMDF 驱动程序中支持 USB 选择性挂起


不是 PPO 的 UMDF 函数驱动程序可以使用基础 WinUSB.sys 驱动程序的功能支持选择性挂起。 UMDF 驱动程序必须通知 WinUSB：设备和驱动程序支持选择性挂起，并必须在 INF 文件中或在 USB 目标设备对象上设置电源策略来启用选择性挂起。

如果 UMDF 函数驱动程序启用选择性挂起，则基础 WinUSB.sys 驱动程序将确定设备何时处于空闲状态。 当没有任何传输处于挂起状态，或者在中断或大容量终结点上仅有等待传输处于传输状态时，WinUSB 将启动空闲超时计数器。 默认情况下，空闲超时值为5秒，但是 UMDF 驱动程序可以更改此默认设置。

当 WinUSB.sys 确定设备处于空闲状态时，它会发送请求以使设备在内核模式设备堆栈中关闭。 总线驱动程序会根据需要更改硬件的状态。 如果端口上的所有设备功能都已被挂起，则该端口进入 USB 选择性挂起状态。

如果在设备挂起时 i/o 请求到达 WinUSB.sys，则 WinUSB.sys 恢复设备操作（如果设备必须为该请求提供服务）。 当系统保留在 S0 中时，UMDF 驱动程序不需要任何代码即可恢复设备。 如果设备硬件可以生成唤醒信号，则 UMDF 驱动程序还可以支持从 S1、S2 或 S3 唤醒系统。 有关详细信息，请参阅 [在 UMDF 驱动程序中唤醒系统](#system-wake-in-a-umdf-driver)。

不是 PPO 的 UMDF 驱动程序可以通过执行以下两个步骤来支持选择性挂起：

1.  通知 WinUSB.sys 设备和驱动程序支持选择性挂起。
2.  启用 USB 选择性挂起。

此外，驱动程序还可以选择：

-   设置设备的超时值。
-   允许用户启用或禁用选择性挂起。

有关如何在不是 PPO 的 UMDF USB 函数驱动程序中实现 USB 选择性挂起的示例，请参阅 \_ WDK 中的 Fx2 驱动程序示例。 此示例位于 **% WinDDK% \\ BuildNumber \\ Src \\ Usb \\ OsrUsbFx2 \\ Umdf \\ Fx2 \_ Driver \\ IdleWake \_ 非 PPO**。

**通知 WinUSB 有关选择性挂起支持的信息**

若要通知 WinUSB.sys 设备是否可以支持 USB 选择性挂起，设备 INF 必须将 DeviceIdleEnabled 值添加到设备的硬件密钥，并将值设置为1。 下面的示例演示了 Fx2 \_ Driver 示例如何在 WUDFOsrUsbFx2 \_ IDLEWAKENON-PPO 文件中添加和设置此值：

```cpp
[OsrUsb_Device_AddReg]
...
HKR,,"DeviceIdleEnabled",0x00010001,1
```

**启用 USB 选择性挂起**

UMDF USB 驱动程序可在运行时或在 INF 中安装期间启用 USB 选择性挂起。

-   若要在运行时启用支持，函数驱动程序将调用 [**IWDFUsbTargetDevice：： SetPowerPolicy**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbtargetdevice-setpowerpolicy) ，并将 PolicyType 参数设置为 AUTO \_ 挂起，并将 Value 参数设置为 TRUE 或1。 下面的示例演示 Fx2 \_ Driver 示例如何在 DeviceNonPpo 文件中启用选择性挂起：
    ```cpp
    BOOL AutoSuspend = TRUE;
    hr = m_pIUsbTargetDevice->SetPowerPolicy( AUTO_SUSPEND,
                                              sizeof(BOOL),
                                             (PVOID) &AutoSuspend );
    ```

-   若要在安装过程中启用支持，INF 包括一个 AddReg 指令，该指令将 DefaultIdleState 值添加到设备的硬件密钥，并将该值设置为1。 例如：
    ```cpp
    HKR,,"DefaultIdleState",0x00010001,1
    ```

**设置空闲超时值**

默认情况下，如果没有任何传输处于挂起状态，或者如果仅挂起传输处于中断或大容量终结点上的传输，则 WinUSB 会在5秒后挂起设备。 UMDF 驱动程序可以在安装时或在运行时更改此空闲超时值。

-   若要在安装时设置空闲超时，INF 包含一个 AddReg 指令，该指令将 DefaultIdleTimeout 值添加到设备的硬件密钥，并将值设置为超时间隔（以毫秒为单位）。 下面的示例将超时设置为7秒：
    ```cpp
    HKR,,"DefaultIdleTimeout",0x00010001,7000
    ```

-   若要在运行时设置空闲超时，驱动程序将调用 **IWDFUsbTargetDevice：： SetPowerPolicy** ，并将 PolicyType 设置为挂起 \_ 延迟，并将值设置为空闲超时值（以毫秒为单位）。 在以下示例中，从设备 .cpp 文件开始，Fx2 \_ 驱动程序示例将超时设置为10秒：
    ```cpp
    HRESULT hr;
    ULONG value;
    value = 10 * 1000;
    hr = m_pIUsbTargetDevice->SetPowerPolicy( SUSPEND_DELAY,
                                              sizeof(ULONG),
                                             (PVOID) &value );
    ```

**为用户控件提供 USB 选择性挂起**

使用 WinUSB 选择性挂起支持的 UMDF USB 驱动程序可选择性地允许用户启用或禁用选择性挂起。 为此，请在 INF 中包含 AddReg 指令，将 UserSetDeviceIdleEnabled 值添加到设备的硬件密钥，并将该值设置为1。 下面显示了用于 AddReg 指令的字符串：

```cpp
HKR,,"UserSetDeviceIdleEnabled",0x00010001,1
```

如果设置了 UserSetDeviceIdleEnabled，设备的 "属性" 对话框将包括 "电源管理" 选项卡，该选项卡允许用户启用或禁用 USB 选择性挂起。

## <a name="system-wake-in-a-umdf-driver"></a>在 UMDF 驱动程序中唤醒系统


在 UMDF 驱动程序中，对系统唤醒的支持与对选择性挂起的支持无关。 UMDF USB 驱动程序可以支持系统唤醒和选择性挂起，无论是系统唤醒还是选择性挂起，或者系统唤醒或选择性挂起。 支持系统唤醒的设备可以将系统从睡眠状态唤醒 (S1、S2 或 S3) 。

UMDF USB PPO 驱动程序可以通过为框架的驱动程序对象提供唤醒信息来支持系统唤醒。 当外部事件触发系统唤醒时，框架会将设备返回到工作状态。

USB 非 PPO 驱动程序可以使用 WinUSB.sys 驱动程序实现的系统唤醒支持。

**若要在 PPO 的 UMDF USB 驱动程序中支持系统唤醒**

用以下参数对框架的设备对象调用 [**IWDFDevice2：： AssignSxWakeSettings**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice2-assignsxwakesettings) 方法：

-   *DxState* 在系统进入可唤醒的 Sx 状态时设备转换到的电源状态。 对于 USB 设备，请将 **PowerDeviceMaximum** 指定为使用总线驱动程序指定的值。
-   如果你的驱动程序允许用户管理唤醒设置或 WakeDoNotAllowUserControl， *UserControlOfWakeSettings*到**WakeAllowUserControl** **。**
-   默认情况下， **WdfUseDefault** *启用唤醒*，但允许用户设置重写默认值。

下面的示例演示 IdleWake \_ PPO 驱动程序如何在其内部的 **CMyDevice：： SetPowerManagement** 方法中调用此方法：

```cpp
hr = m_FxDevice->AssignSxWakeSettings( PowerDeviceMaximum,
                                       WakeAllowUserControl,
                                       WdfUseDefault);
```

**在非 PPO 驱动程序中通过 WinUSB 启用系统唤醒**

若要启用通过 WinUSB 的系统唤醒，驱动程序的 INF 会将注册表值 SystemWakeEnabled 添加到设备的硬件密钥，并将其设置为1。 IdleWake \_ 非 PPO 示例启用系统唤醒，如下所示：

```cpp
[OsrUsb_Device_AddReg]
...
HKR,,"SystemWakeEnabled",0x00010001,1
```

通过设置此值，驱动程序将启用系统唤醒，并允许用户控制设备唤醒系统的能力。 在设备管理器中，设备的 "电源管理设置" 属性页包含一个复选框，用户可以在其中启用或禁用系统唤醒。

## <a name="related-topics"></a>相关主题
[USB 驱动程序 (WDF) 中的选择性挂起](selective-suspend-in-usb-drivers-wdf.md)  



