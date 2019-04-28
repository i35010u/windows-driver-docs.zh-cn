---
Description: 本主题介绍如何 UMDF 函数驱动程序支持 USB 选择性挂起。
title: 在 USB UMDF 驱动程序的选择性挂起
ms.date: 05/09/2018
ms.localizationpriority: medium
ms.openlocfilehash: 9e8103a70187fdac429671a5b6296edd8e314cfb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331079"
---
# <a name="selective-suspend-in-usb-umdf-drivers"></a>在 USB UMDF 驱动程序的选择性挂起


**重要的 Api**

-   [**IWDFUsbTargetDevice::SetPowerPolicy**](https://msdn.microsoft.com/library/windows/hardware/ff560385)
-   [**IWDFDevice2::AssignSxWakeSettings**](https://msdn.microsoft.com/library/windows/hardware/ff556923)
-   [**IWDFDevice2::AssignS0IdleSettings**](https://msdn.microsoft.com/library/windows/hardware/ff556920)

本主题介绍如何 UMDF 函数驱动程序支持 USB 选择性挂起。

UMDF 函数驱动程序可以支持 USB 选择性挂起中通过两种方式：

-   通过声明的电源策略所有权和处理设备空闲关机和恢复。
-   通过依赖 WinUSB.sys 驱动程序，Microsoft 提供，以处理选择性挂起。 WinUSB.sys UMDF USB 驱动程序在安装期间作为内核模式设备堆栈的一部分安装。 WinUSB.sys 实现挂起和继续执行 USB 设备操作的基础机制。

这两种方法需要仅少量的代码。 WDK 中提供的 IdleWake 示例演示如何支持选择性挂起 UMDF USB 驱动程序中。 您可以在 %winddk%中找到此示例\\BuildNumber\\Src\\Usb\\OsrUsbFx2\\ UMDF\\Fx2\_驱动程序\\IdleWake。 文件夹包含 PPO 和非 PPO 版本的示例。

支持选择性挂起的 UMDF 驱动程序必须遵循以下准则：

-   UMDF 驱动程序可以声明为其设备堆栈，电源策略所有权，但不要求必须这样做。 默认情况下，基础 WinUSB.sys 驱动程序拥有电源策略。
-   支持选择性的 UMDF 驱动程序挂起和是 PPO 可以使用电源管理的队列或队列不电源管理的。 UMDF 驱动程序支持选择性挂起，但不是 PPO 一定不能使用电源管理队列。

## <a name="power-policy-ownership-in-umdf-usb-drivers"></a>在 UMDF USB 驱动程序中的电源策略所有权


默认情况下，WinUSB.sys 是包含 UMDF USB 驱动程序的设备堆栈 PPO。 从 WDF 1.9 开始，基于 UMDF 的 USB 驱动程序可以声明所有权，电源策略。 由于每个设备堆栈中的只有一个驱动程序可以是 PPO，PPO 的 UMDF USB 驱动程序必须显式禁用 WinUSB.sys 中的电源策略所有权。

**若要声明 UMDF USB 驱动程序中的电源策略所有权**

1.  调用**IWDFDeviceInitialize::SetPowerPolicyOwnership** ，并将传递**TRUE**，通常是从**IDriverEntry::OnDeviceAdd**驱动程序回调对象上的方法。 例如：

    ``` syntax
    FxDeviceInit->SetPowerPolicyOwnership(TRUE);
    ```

2.  禁用 WinUSB 中的电源策略所有权。 在驱动程序的 INF 文件中，包括**AddReg**设置的指令**WinUsbPowerPolicyOwnershipDisabled**中为非零值的注册表值。 **AddReg**指令必须出现在 DDInstall.HW 部分。 例如：

    ``` syntax
    [MyDriver_Install.NT.hw]
    AddReg=MyDriver_AddReg

    [MyDriver_AddReg]
    HKR,,"WinUsbPowerPolicyOwnershipDisabled",0x00010001,1
    ```

支持选择性的 UMDF USB 驱动程序挂起，并生成与 WDF 版本早于 1.9 不得声明电源策略所有权。 WDF 这些早期版本中，USB 选择性挂起的工作原理正确才 WinUSB.sys PPO。

## <a name="io-queues-in-umdf-usb-drivers"></a>UMDF USB 驱动程序中的 I/O 队列


UMDF 驱动程序支持选择性挂起，是否 UMDF 驱动程序拥有其设备的电源策略确定它可以使用的 I/O 队列的类型。 支持选择性的 UMDF 驱动程序挂起和 PPOs 可以使用电源管理或电源管理的队列。 支持选择性的 UMDF USB 驱动程序挂起，但不 PPO 不应使用任何电源管理的 I/O 队列。

如果设备被挂起时，I/O 请求到达的电源管理的队列时，框架不会带来请求驱动程序是 PPO，除非在图中所示[USB 驱动程序中的选择性挂起](https://msdn.microsoft.com/library/windows/hardware/dn449739)。 如果 UMDF 驱动程序不是设备 PPO，框架无法代表自己设备接通电源。 因此，请求将保留在电源管理队列中卡住。 请求永远不会到达 WinUSB，因此 WinUSB 无法在设备接通电源。 因此，可以停止设备堆栈。

如果队列不是电源管理，框架提供了对 UMDF 驱动程序的 I/O 请求，即使设备已关闭。 UMDF 驱动程序格式化请求，并按常规方式将其转发到默认 I/O 目标设备堆栈下。 不需要特殊的代码。 当请求到达 PPO (WinUSB.sys) 时，WinUSB.sys 将启动设备并执行所需的 I/O 操作。

中的示例驱动程序 **%winddk%\\BuildNumber\\Src\\Usb\\OsrUsbFx2\\umdf\\Fx2\_驱动程序\\IdleWake**定义常量\_不\_电源\_策略\_所有者\_生成非 PPO 版本的驱动程序时。 当驱动程序创建一个队列进行读取和写入请求时，它确定是否通过检查该常量来创建电源管理的队列。

若要创建队列，该驱动程序调用的驱动程序定义**CMyQueue::Initialize**方法，它使用以下三个参数：

-   *DispatchType*，WDF\_IO\_队列\_调度\_类型枚举值，该值指示队列发送请求的方式。
-   *默认*，一个布尔值，该值指示队列是否为默认队列。
-   *PowerManaged*，一个布尔值，该值指示队列是否为电源管理。

下面的代码段显示了驱动程序的调用**CMyQueue::Initialize**读写队列创建过程的方法：

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

**CMyQueue::Initialize**然后调用[ **IWDFDevice::CreateIoQueue** ](https://msdn.microsoft.com/library/windows/hardware/ff557020)以创建队列，如下所示：

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

此代码序列会导致将调度并行请求的默认队列。 如果驱动程序 PPO 队列是否电源管理，以及是否驱动程序不是 PPO，队列不是电源管理。

## <a name="supporting-usb-selective-suspend-in-a-umdf-ppo"></a>在 UMDF PPO 支持 USB 选择性挂起


为支持选择性挂起，其设备堆栈必须执行以下操作是 PPO UMDF USB 驱动程序：

1.  通常中声明的设备堆栈电源策略所有权[ **IDriverEntry::OnDeviceAdd** ](https://msdn.microsoft.com/library/windows/hardware/ff554896)上其驱动程序回调对象，如前面所述的方法。
2.  通过调用启用选择性挂起[ **IWDFDevice2::AssignS0IdleSettings** ](https://msdn.microsoft.com/library/windows/hardware/ff556920) framework 设备对象的方法。

**若要启用 USB 选择性挂起来自 PPO**

-   调用[ **IWDFDevice2::AssignS0IdleSettings**](https://msdn.microsoft.com/library/windows/hardware/ff556920)，通常是从**OnPrepareHardware**设备回调对象的方法。 将参数设置为 AssignS0IdleSettings，如下所示：
    -   *IdleCaps*到**IdleUsbSelectiveSuspend**。
    -   *DxState*到框架转换空闲状态的设备的设备睡眠状态。 有关 USB 选择性挂起，指定**PowerDeviceMaximum**，指示框架应使用总线驱动程序指定的值。
    -   *IdleTimeout*为的毫秒数中设备必须保持空闲之前 framework 转换到*DxState*。
    -   *UserControlOfIdleSettings*到**IdleAllowUserControl**如果您的驱动程序允许用户管理的空闲状态的设置，或到其他**IdleDoNotAllowUserControl**。
    -   *已启用*到**WdfUseDefault**若要启用选择性挂起默认情况下，但若要允许用户的设置来覆盖默认值。

下面的示例演示如何 IdleWake\_PPO 驱动程序在其内部 CMyDevice::SetPowerManagement 方法中调用此方法：

```cpp
hr = m_FxDevice->AssignS0IdleSettings( IdleUsbSelectiveSuspend,
                                PowerDeviceMaximum,
                                IDLE_TIMEOUT_IN_MSEC,
                                IdleAllowUserControl,
                                WdfUseDefault);                                                                                                   
```

如果设备硬件可以生成唤醒信号，UMDF 驱动程序还可以从 S1、 S2 或 S3 支持系统唤醒。 有关详细信息，请参阅[UMDF 驱动程序中唤醒系统](#systemwake)。

## <a name="supporting-usb-selective-suspend-in-a-non-ppo-umdf-driver"></a>PPO UMDF 驱动程序中支持 USB 选择性挂起


通过使用基础 WinUSB.sys 驱动程序的功能不是 PPO 可以支持选择性的 UMDF 函数驱动程序挂起。 UMDF 驱动程序必须通知 WinUSB 设备和驱动程序支持选择性挂起，并且必须启用选择性挂起 INF 文件中或通过 USB 目标设备对象上设置电源策略。

如果 UMDF 功能驱动程序启用了选择性挂起，基础 WinUSB.sys 驱动程序将确定该设备处于空闲状态时。 WinUSB 启动空闲超时计数器没有划转挂起或在仅挂起传输都是在中断或大容量的终结点上的传输。 默认情况下，空闲超时值为 5 秒，但 UMDF 驱动程序可以更改此默认值。

当 WinUSB.sys 确定设备处于空闲状态时，它将发送挂起内核模式设备堆栈的下层设备的请求。 总线驱动程序更改为适当的硬件的状态。 如果所有设备的端口上的函数已被挂起，该端口将都进入 USB 选择性挂起状态。

如果设备被挂起时，I/O 请求到达时在 WinUSB.sys，WinUSB.sys 恢复设备操作，如果设备还必须启动为请求提供服务。 UMDF 驱动程序不需要任何代码来恢复该设备，而系统仍然处于 S0。 如果设备硬件可以生成唤醒信号，UMDF 驱动程序还可以从 S1、 S2 或 S3 支持系统唤醒。 有关详细信息，请参阅[UMDF 驱动程序中唤醒系统](#systemwake)。

不是 PPO 可以支持选择性的 UMDF 驱动程序挂起通过采用以下两个步骤：

1.  通知 WinUSB.sys 设备和驱动程序支持选择性挂起。
2.  启用 USB 选择性挂起。

此外，驱动程序可以 （可选）：

-   设置设备的超时值。
-   允许用户启用或禁用选择性挂起。

举例说明如何实现 USB 选择性挂起不是 PPO UMDF USB 功能驱动程序中，请参阅 Fx2\_WDK 中的驱动程序示例。 此示例位于 **%winddk%\\BuildNumber\\Src\\Usb\\OsrUsbFx2\\Umdf\\Fx2\_驱动程序\\IdleWake\_非 PPO**。

**以通知有关选择性 WinUSB 挂起支持**

若要通知 WinUSB.sys 设备可以支持 USB 选择性挂起，设备 INF 必须将 DeviceIdleEnabled 值添加到设备的硬件密钥并将值设置为 1。 下面的示例演示如何 Fx2\_驱动程序示例将添加并将此值设置在 WUDFOsrUsbFx2\_IdleWakeNon PPO.Inx 文件：

```cpp
[OsrUsb_Device_AddReg]
...
HKR,,"DeviceIdleEnabled",0x00010001,1
```

**若要启用 USB 选择性挂起**

UMDF USB 驱动程序可以启用 USB 选择性挂起在运行时或在 INF 的安装过程。

-   若要启用支持在运行时，功能驱动程序调用[ **IWDFUsbTargetDevice::SetPowerPolicy** ](https://msdn.microsoft.com/library/windows/hardware/ff560385)并 PolicyType 参数设置为自动\_挂起和 Value 参数为 TRUE 或 1。 下面的示例演示如何 Fx2\_驱动程序示例启用选择性挂起 DeviceNonPpo.cpp 文件中：
    ```cpp
    BOOL AutoSuspend = TRUE;
    hr = m_pIUsbTargetDevice->SetPowerPolicy( AUTO_SUSPEND,
                                              sizeof(BOOL),
                                             (PVOID) &AutoSuspend );
    ```

-   若要在安装过程中启用支持，INF 包括一个 AddReg 指令将 DefaultIdleState 值添加到设备的硬件密钥并将值设置为 1。 例如：
    ```cpp
    HKR,,"DefaultIdleState",0x00010001,1
    ```

**若要设置空闲超时值**

如果没有传输处于挂起状态或 WinUSB 5 秒后该设备的挂起默认情况下，仅挂起传输都是在中断或大容量的终结点上的传输。 UMDF 驱动程序可以更改此空闲超时值在 INF 的安装时或在运行时。

-   若要在安装时设置空闲超时，INF 包括一个 AddReg 指令将 DefaultIdleTimeout 值添加到设备的硬件密钥并将值设置为以毫秒为单位的超时间隔。 下面的示例设置为 7 秒超时值：
    ```cpp
    HKR,,"DefaultIdleTimeout",0x00010001,7000
    ```

-   若要在运行时，驱动程序调用设置空闲超时**IWDFUsbTargetDevice::SetPowerPolicy**与设置为挂起的 PolicyType\_延迟，并为空闲超时值，以毫秒为单位的值。 在下面的示例从 Device.cpp 文件 Fx2\_驱动程序示例设置为 10 秒的超时值：
    ```cpp
    HRESULT hr;
    ULONG value;
    value = 10 * 1000;
    hr = m_pIUsbTargetDevice->SetPowerPolicy( SUSPEND_DELAY,
                                              sizeof(ULONG),
                                             (PVOID) &value );
    ```

**若要提供用户控件的 USB 选择性挂起**

UMDF USB 驱动程序使用 WinUSB 选择性挂起支持 （可选） 可以允许用户启用或禁用选择性挂起。 若要执行此操作，包括中 INF 将 UserSetDeviceIdleEnabled 值添加到设备的硬件密钥并将值设置为 1 AddReg 指令。 下面显示了要使用 AddReg 指令的字符串：

```cpp
HKR,,"UserSetDeviceIdleEnabled",0x00010001,1
```

如果设置 UserSetDeviceIdleEnabled，设备的属性对话框包括选项卡允许用户启用或禁用 USB 选择性挂起电源管理。

## <a name="system-wake-in-a-umdf-driver"></a>在 UMDF 驱动程序中的系统唤醒


在 UMDF 驱动程序，对系统唤醒是独立于支持支持选择性挂起。 UMDF USB 驱动程序可以支持这两个系统唤醒和选择性挂起，既不系统唤醒也选择性挂起，或任一系统唤醒或选择性挂起。 支持系统项的设备可以唤醒从睡眠状态 （S1、 S2 或 S3） 系统。

USB PPO UMDF 驱动程序可以通过提供框架的驱动程序对象的唤醒信息的支持系统唤醒。 当外部事件触发时系统被唤醒时，框架会将设备返回到工作状态。

USB 非 PPO 驱动程序可以使用 WinUSB.sys 驱动程序实现的系统唤醒支持。

**这是 PPO 到 UMDF USB 驱动程序中支持系统唤醒**

调用[ **IWDFDevice2::AssignSxWakeSettings** ](https://msdn.microsoft.com/library/windows/hardware/ff556923)框架的设备对象，使用以下参数的方法：

-   *DxState*到的设备转换时的电源状态系统进入可唤醒 Sx 状态。 适用于 USB 设备，指定**PowerDeviceMaximum**使用总线驱动程序指定的值。
-   *UserControlOfWakeSettings*到**WakeAllowUserControl**如果您的驱动程序允许用户管理唤醒设置或其他到**WakeDoNotAllowUserControl。**
-   *已启用*到**WdfUseDefault**以启用唤醒，默认情况下，而是允许用户的设置来覆盖默认值。

下面的示例演示如何 IdleWake\_PPO 驱动程序调用此方法在其内部**CMyDevice::SetPowerManagement**方法：

```cpp
hr = m_FxDevice->AssignSxWakeSettings( PowerDeviceMaximum,
                                       WakeAllowUserControl,
                                       WdfUseDefault);
```

**若要启用通过 WinUSB 系统唤醒中非 PPO 驱动程序**

若要启用通过 WinUSB 系统被唤醒，驱动程序的 INF 将注册表值 SystemWakeEnabled 添加到设备的硬件密钥，并将其设置为 1。 IdleWake\_非 PPO 示例使系统被唤醒，如下所示：

```cpp
[OsrUsb_Device_AddReg]
...
HKR,,"SystemWakeEnabled",0x00010001,1
```

通过设置此值，该驱动程序同时启用系统唤醒，并允许用户可以控制设备能够将系统唤醒。 在设备管理器中，设备的电源管理设置属性页包含与该用户可以启用或禁用系统唤醒一个复选框。

## <a name="related-topics"></a>相关主题
[USB 驱动程序 (WDF) 中的选择性挂起](selective-suspend-in-usb-drivers-wdf.md)  



