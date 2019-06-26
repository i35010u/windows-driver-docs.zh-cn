---
title: SoC 上 PWM 模块的 PWM 驱动程序
description: PWM 控制器属于 SoC 和到 SoC 地址空间，内存映射。 编写操作 PWM 的内核模式驱动程序注册，并提供对应用程序的访问。
ms.assetid: 911375A9-6761-45C1-BB5E-79BC0E4409AC
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3f1bbeb1a4550f2f967088e44575a22408161717
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386303"
---
# <a name="pwm-driver-for-an-on-soc-pwm-module"></a>SoC 上 PWM 模块的 PWM 驱动程序
提供访问脉冲的宽度调整 (PWM) 控制器属于 SoC 和 SoC 地址空间为内存映射，需要编写器的内核模式驱动程序。 该驱动程序必须注册的设备类接口的 PWM 控制器，以便 UWP 应用可以访问系统公开 PWM 设备通过 PWM WinRT Api Windows.Devices.Pwm 命名空间中定义。 

**请注意**如果您有一个外接程序 PWM 模块，通过我<sup>2</sup>C、 SPI 或 UART 控制器，你可以访问该模块从 UWP 应用使用 Api 中定义的[ **Windows.Devices.Pwm**](https://docs.microsoft.com/uwp/api/windows.devices.pwm)并[ **Windows.Devices.Pwm.Provider** ](https://docs.microsoft.com/uwp/api/windows.devices.pwm.provider)命名空间。 

PWM 设备已抽象化为一个控制器和一个或多个 pin。 控制在控制器或球瓶均通过 PWM 定义 Ioctl。 例如，LCD 显示器驱动程序将此类请求发送到 PWM 驱动程序来控制 LCD 背景光级别。 

多控制器和多渠道 PWM 信号生成与可配置的段、 极性和关税周期这样的以下任务： 

-   驱动器伺服电动机。 
-   像 LED 或 DC 碰电机驱动器负载。 
-   生成模拟信号。 
-   生成精确的时钟。 

本主题介绍了， 

-   如何启用 UWP 设备的访问权限系统公开 PWM。 

-   如何处理 PWM IOCTL 请求发送的 Win32 应用程序或第三方内核模式驱动程序。

**目标的受众**

-   Oem 和 Ihv 开发具有在 SoC PWM 控制器的系统。 

**上次更新时间**

-   2017 年 8 月

**Windows 版本**

-   Windows 10 版本

**重要的 API**

-   [PWM Ioctl](https://docs.microsoft.com/windows/desktop/DevIO/pwm-api)

## <a name="about-pwm"></a>有关 PWM
PWM 介绍用于生成矩形 pulse 批调制的 pulse 宽度导致波形的平均值的变体的基本方法。  

PWM 波形可按两个参数进行分类： 波形周期 (T) 和占空比。 波形频率 (f) 是波形段 f 倒数 = 1/t。 占空比介绍的 on 或固定时间间隔或时间范围内的 'Active' 时间的比例因为电源已关闭的大多数情况下，低占空比对应于低输出电源的平均值。 占空比以百分比表示，其中 100%完全在正在被完全关闭，正在 50%的时间的活动的 50%的 0%。

![“驱动程序”](images/pwm.png)


## <a name="accessing-the-system-exposed-pwm-controller-and-pins"></a>访问系统公开 PWM 控制器和 pin

必须注册 PWM 驱动程序  
GUID_DEVINTERFACE_PWM_CONTROLLER 作为设备接口来公开和访问 PWM 设备的 GUID。 

```cpp
// {60824B4C-EED1-4C9C-B49C-1B961461A819} 

DEFINE_GUID(GUID_DEVINTERFACE_PWM_CONTROLLER, 0x60824b4c, 0xeed1, 0x4c9c, 0xb4, 0x9c, 0x1b, 0x96, 0x14, 0x61, 0xa8, 0x19); 

#define GUID_DEVINTERFACE_PWM_CONTROLLER_WSZ L"{60824B4C-EED1-4C9C-B49C-1B961461A819}" 
```

若要注册设备接口的 GUID，该驱动程序必须在驱动程序的实现中 EVT_WDF_DRIVER_DEVICE_ADD 回调函数的调用 WdfDeviceCreateDeviceInterface。 注册后，系统向控制器和球瓶分配的符号链接。

应用程序或另一个驱动程序可以控制是在控制器或通过 PWM 球瓶定义 Ioctl。 在发送前 Ioctl，发件人应用程序或驱动程序必须打开的文件句柄在控制器和 pin 通过指定其符号链接。 这需要驱动程序注册为文件创建和关闭事件。 请参阅 （链接） 


下面是在控制器的符号路径的示例：
```cpp
\??\ACPI#FSCL000E#1#{60824b4c-eed1-4c9c-b49c-1b961461a819}  
```
同样，球瓶的格式如下所示：路径的格式如下所示：

```cpp
<DeviceInterfaceSymbolicLinkName>\<PinNumber>
```
其中<PinNumber>是基于 0 的 pin 来打开的索引。 

下面是插针的符号路径的示例：
```cpp
\??\ACPI#FSCL000E#1#{60824b4c-eed1-4c9c-b49c-1b961461a819}\0 ; Opens pin 0 

\??\ACPI#FSCL000E#1#{60824b4c-eed1-4c9c-b49c-1b961461a819}\0001 ; Opens pin 1 with the leading 0s have no effect.
```

若要打开的文件句柄，该应用程序必须调用配置管理器 Api （CM_Get_Device_Interface_ *）。 

打开的文件句柄后，应用程序可以通过调用 DeviceIoControl 函数发送这些请求。 请参阅 PWM 部分。



该驱动程序应使用提供的 PWM 支持例程 PwmParsePinPath 来分析和验证 pin 路径并提取的 pin 号码。 

## <a name="setting-device-interface-properties"></a>设置设备接口属性

若要从 UWP 应用使用 PWM WinRT Api 这些[设备接口属性](https://docs.microsoft.com/previous-versions/ff541409(v=vs.85))必须设置。

-   [DEVPKEY_DeviceInterface_Restricted](https://docs.microsoft.com/windows-hardware/drivers/install/devpkey-deviceinterface-restricted) 

    根据当前的 UWP 设备访问模型设置为 FALSE 的受限的设备接口属性需要让 PWM 设备接口的 UWP 应用访问。   

-   DEVPKEY_DeviceInterface_SchematicName （链接???）

    将示意名称分配给 PWM 设备接口以静态方式互联 PWM 设备都需要使用 PwmController.GetDeviceSelector(FriendlyName) 工厂方法。 示意图名称是提供给系统设计图表，例如 （PWM0，PWM_1，et...） 中的 PWM 设备的名称。 假定示意名称是唯一的系统，但不是会执行。 至少，应该不会有 2 个 PWM 设备具有相同的示意名称，否则 WinRT PWM PwmController.GetDeviceSelector(FriendlyName) 行为将为非确定性。 

可以通过两种方式之一设置属性：

1. 使用用于 PWM 驱动程序 INF 文件

   使用**AddProperty**指令设置设备属性。 应允许 INF 文件上的一个或 PWM 设备实例子集设置不同的值相同的属性。 下面是设置 DEVPKEY_DeviceInterface_Restricted 的示例。
    ```cpp
    ;***************************************** 
    ; Device interface installation 
    ;***************************************** 

    [PWM_Device.NT.Interfaces] 
    AddInterface={60824B4C-EED1-4C9C-B49C-1B961461A819},,PWM_Interface 

    [PWM_Interface] 
    AddProperty=PWM_Interface_AddProperty 

    ; Set DEVPKEY_DeviceInterface_Restricted property to false to allow UWP access 
    ; to the device interface without the need to be bound with device metadata. 
    ; If Restricted property is set to true, then only applications which are bound 
    ; with device metadata would be allowed access to the device interface. 

    [PWM_Interface_AddProperty] 
    {026e516e-b814-414b-83cd-856d6fef4822},6,0x11,,0 
    ```
    并非所有的设计中，还有用于公开到 UWP PWM 设备相同的策略。 例如，该策略可能以允许 UWP PWM 设备实例子集的访问。 公开 PWM 设备的子集，或将不同的属性值分配给一个或一部分 PWM 设备实例需要为每个 PWM 设备实例和匹配 INF 部分有选择地根据策略的不同硬件 ID。

    考虑的基于 SoC 设计其中存在是四个相同 PWM 设备命名的实例 （IP 块） PWM0，...，PWM3 其 ACPI 分配硬件 ID (_HID) 的位置是 FSCL00E0，其唯一 ID (_UID) 为 0，...，3。 公开到 UWP 的所有 PWM 设备将需要设置的硬件 ID ACPI\FSCL00E0 DEVPKEY_DeviceInterface_Restricted 以匹配的 INF 部分。 

    这种方式设置属性不需要的驱动程序代码中的任何更改。 这是更简单的方法作为服务 INF 文件比更容易驱动程序二进制文件。 代价是这种方法需要为每个设计的定制的 INF 文件。 


2.  以编程方式在 PWM 驱动程序 

    PWM 驱动程序可以调用 IoSetDeviceInterfacePropertyData 后它会创建并发布 PWM 设备接口在其 EVT_WDF_DRIVER_DEVICE_ADD 实现中设置设备接口属性。 该驱动程序负责决定要分配的值和设备属性。 该信息通常存储在基于 SoC 设计的 ACPI 系统。 每个设备接口属性的值可以指定每个 ACPI 设备节点 _DSD 方法中，为设备属性。 驱动程序必须查询从 ACPI _DSD、 分析设备属性数据、 提取每个属性的值，并将其分配设备接口。 

    以编程方式设置属性使驱动程序和其 INF 文件可移植性跨设计，因此 Bsp 更改只会在 ACPI DSDT 定义每个 PWM 设备节点中。 但是，读取和分析 ACPI 二进制块会很麻烦，并且需要大量的代码可以是容易出现错误和生成更大的错误图面中的漏洞。 

## <a name="handling-file-openclose-events"></a>处理文件打开/关闭事件

PWM 驱动程序需要注册为文件创建和关闭事件通过实现 EVT_WDF_DEVICE_FILE_CREATE 和 EVT_WDF_FILE_CLEANUP/EVT_WDF_FILE_CLOSE 回调函数。 在实现中，该驱动程序必须执行以下任务：

1.  确定是否创建请求的控制器或 pin。 
2.  如果请求 pin，则驱动程序必须分析和验证 pin 路径创建 pin 请求并确保请求的 pin 号是控制器的边界内。 
3.  授予或拒绝访问控制器和插针创建请求。 
4.  维护每个定义完善的状态机的控制器和 pin 状态完整性。 

在前面的任务集，可以按如下所示在 EVT_WDF_DEVICE_FILE_CREATE 中, 执行验证的第二个任务：

1. 如果与请求文件对象相关联的文件名为 null，然后完成该请求与 STATUS_INVALID_DEVICE_REQUEST。 

2. 如果与请求文件对象相关联的文件名为空字符串，则这是一个控制器创建请求，否则它是 pin 创建请求。 

3. 如果这是一个 pin 创建请求，然后： 

    1. 分析的格式的固定路径\<DecimalName >，并通过调用 PwmParsePinPath 解压缩的 pin 号码。 

    2. 如果分析和验证失败的 pin 路径，完成与 STATUS_NO_SUCH_FILE 请求。 

    3. 如果 pin 号是大于或等于控制器固定计数，然后完成 STATUS_NO_SUCH_FILE 的请求。 请注意，pin 号是从零开始的索引。 

    4. 否则，继续处理 EVT_WDF_DEVICE_FILE_CREATE。 

下面是示例代码 EVT_WDF_DEVICE_FILE_CREATE 处理程序，实现前面提到的验证步骤： 

```cpp
EVT_WDF_DEVICE_FILE_CREATE PwmEvtDeviceFileCreate;

VOID 

PwmEvtDeviceFileCreate ( 
    WDFDEVICE WdfDevice, 
    WDFREQUEST WdfRequest, 
    WDFFILEOBJECT WdfFileObject 
    ) 
{ 

    UNICODE_STRING* filenamePtr = WdfFileObjectGetFileName(WdfFileObject); 
    IMXPWM_DEVICE_CONTEXT* deviceContextPtr = PwmGetDeviceContext(WdfDevice); 
    NTSTATUS status; 
    ULONG pinNumber; 

    // 
    // Parse and validate the filename associated with the file object 
    // 

    bool isPinInterface; 

    if (filenamePtr == nullptr) { 

        WdfRequestComplete(WdfRequest, STATUS_INVALID_DEVICE_REQUEST); 

        return; 

    } else if (filenamePtr->Length > 0) { 

        // 
        // A non-empty filename means to open a pin under the controller namespace 
        // 

        status = PwmParsePinPath(filenamePtr, &pinNumber); 

        if (!NT_SUCCESS(status)) { 

            WdfRequestComplete(WdfRequest, status); 

            return; 

        } 


        if (pinNumber >= deviceContextPtr->ControllerInfo.PinCount) { 

            WdfRequestComplete(WdfRequest, STATUS_NO_SUCH_FILE); 

            return; 

        } 


        isPinInterface = true; 

    } else { 

        // 
        // An empty filename means that the create is against the root controller 
        // 

        isPinInterface = false; 
    } 

    // 
    // Continue request processing here 
    // 
} 
```
### <a name="controller-and-pin-sharing"></a>控制器和 pin 共享 

控制器和 pin 的共享模式遵循多个读取器，单个编写器模式。 控制器/pin 可由多个调用方，打开进行读取，但只有一个调用方可以写入一次打开该控制器/pin。 

可以通过打开文件句柄时使用的所需的访问和共享访问标志的组合实现该模型。 只有所需的访问规范用于控制访问更简单的共享语义 opts DDI 共享模型。 共享访问规范不能共享模型中播放的任何角色，并为如果指定打开控制器或 pin 时遵循。  

在 EVT_WDF_DEVICE_FILE_CREATE，创建请求所需的访问和共享访问应提取或验证基于控制器/pin 状态或按如下所示： 

1. 如果共享访问不是 0，则拒绝访问和使用 STATUS_SHARING_VIOLATION 完整的请求。 

2. 如果所需的访问是为读取的则授予访问权限，并继续处理 EVT_WDF_DEVICE_FILE_CREATE。 

3. 如果所需的访问以进行写入，则： 

如果控制器/pin 已打开以进行写入，然后又拒绝访问，并完成该请求与 STATUS_SHARING_VIOLATION、 else 授予访问权限、 标记的控制器或 pin，如打开以进行写入和继续处理 EVT_WDF_DEVICE_FILE_CREATE。 

下面是一个示例演示如何从创建请求中提取所需的访问权限和共享访问权限： 

```cpp
void 
PwmCreateRequestGetAccess( 
    _In_ WDFREQUEST WdfRequest, 
    _Out_ ACCESS_MASK* DesiredAccessPtr, 
    _Out_ ULONG* ShareAccessPtr 
    ) 
{ 

    NT_ASSERT(ARGUMENT_PRESENT(DesiredAccessPtr)); 

    NT_ASSERT(ARGUMENT_PRESENT(ShareAccessPtr)); 


    WDF_REQUEST_PARAMETERS wdfRequestParameters; 

    WDF_REQUEST_PARAMETERS_INIT(&wdfRequestParameters); 

    WdfRequestGetParameters(WdfRequest, &wdfRequestParameters); 


    NT_ASSERTMSG( 

        "Expected create request", 
        wdfRequestParameters.Type == WdfRequestTypeCreate); 


    *DesiredAccessPtr = 
        wdfRequestParameters.Parameters.Create.SecurityContext->DesiredAccess; 

    *ShareAccessPtr = wdfRequestParameters.Parameters.Create.ShareAccess; 
} 
```

### <a name="controller-and-pin-independence"></a>控制器和 pin 独立性

控制器和 pin 具有父-子图片。 若要打开 pin，必须首先打开其父控制器。 另一种方法是查看插针是作为独立的实体，其父控制器提供 pin，这在该控制器上设置所包含的所有 pin 的全局 PWM 期到只有一个服务。 

以下是一些示例方案： 

- 单个进程的访问权限： 

    -   进程 A 可以打开 pin、 设置其占空比、 启动它使用控制器默认期限和更高版本打开控制器和按需设置其期限。 它可能永远不需要打开控制器，如果默认期限为应用程序是确定。 

    -   一个过程可以有多个控制不同的 pin，同一个控制器下每个线程的位置。 

- 多进程的访问权限： 

    -   命令行实用程序可以使用用于显示到控制台的信息的只读访问权限打开控制器。 同时在后台 UWP 任务可以写入打开控制器、 控制某些 LED 与单个插针。 

    -   写入包含在控制器和锁定 PWM 段时控制通过 Pin0 LCD 背景光内核模式显示驱动程序。 同时，Win32 服务使用 PWM 段由显示器驱动程序设置，并且使用 Pin1 dim 一些导致来某些状态传达给用户。 

请注意，有一些重要的影响到打开和关闭独立于其插针，控制器。 有关详细信息，请参阅状态机的一部分。 

## <a name="controller-and-pin-state-machines"></a>控制器和 pin 的状态机

**控制器状态定义**

|状态的功能|默认值|描述|
|---|---|--|
|Is-Opened-For-Write|False| False 表示控制器或者已关闭或打开以进行读取;True 指示它打开以进行写入。|
|所需的时间| MinimumPeriod| |

![控制器状态机](images/controller-state-machine.png)

下面的控制器状态机被以只是打开的-写状态。 所需时间段值是还省略，因为它不会影响可以在控制器执行的操作的类型。 请注意，每当打开进行写入的控制器获取打开以进行写入的调用方已关闭，控制器会重置为其默认值 （所需的默认期限）。

**Pin 状态定义**


|    状态的功能    | 默认值 |                                                   描述                                                    |
|---------------------|---------------|------------------------------------------------------------------------------------------------------------------|
| Is-Opened-For-Write |     False     | False 表示 pin 或者已关闭或打开以进行读取;True 指示它打开以进行写入。 |
|  Active-Duty-Cycle  |       0       |                                                                                                                  |
|     Is-Started      |     False     |                                 False 表示已停止;True 表示已启动。                                 |

![Pin 状态机](images/pins-state-machine.png)

Pin 状态机以两种状态是打开的-写，并且已启动的组合为中心。 活动的工作周期省略，因为它们的值不会影响的操作可以执行的插针的类型和其他 pin 状态等极性。 请注意，每当打开以进行写入的调用方获取关闭写入打开的 pin，pin 收到 rest 为其默认值 （已停止，默认极性和 active 占空比）。 另请注意已启动的状态在该集极性转换 = true 省略了，因为它处于无效状态。

给定的状态未提及的任何转换意味着，此类转换是无效或不可能的相应的请求应已完成，但相应的错误状态。 

### <a name="implementation-considerations-for-state-transitions"></a>状态转换的实现注意事项

- 在 EVT_WDF_DEVICE_FILE_CREATE，驱动程序应授予或拒绝访问，如下所示基于创建请求所需的访问权限和控制器或 pin 是打开的-写状态：

    如果请求具有所需的写访问权限，并且控制器/pin 已打开以进行写入，则完成该请求与 STATUS_SHARING_VIOLATION，否则将标记控制器/pin 为打开以进行写入 (是打开的-写 = true)，授予访问权限并继续正在处理。

    此示例中实现上述的访问验证步骤，用于省略必要的锁定逻辑来处理并发文件在其中创建请求的 EVT_WDF_DEVICE_FILE_CREATE 处理程序： 
    ```cpp
    //
    // Verify request desired access
    //

    const bool hasWriteAccess = desiredAccess & FILE_WRITE_DATA;

    if (isPinInterface) {
        PWM_PIN_STATE* pinPtr = deviceContextPtr->Pins + pinNumber;
        if (hasWriteAccess) {
            if (pinPtr->IsOpenForReadWrite) {
                PWM_LOG_TRACE("Pin%lu access denied.", pinNumber);
                WdfRequestComplete(WdfRequest, STATUS_SHARING_VIOLATION);
                return;
            }
            pinPtr->IsOpenForReadWrite = true;
        }
        PWM_LOG_TRACE(
            "Pin%lu Opened. (IsOpenForReadWrite = %lu)",
            pinNumber,
            (pinPtr->IsOpenForReadWrite ? 1 : 0));

    } else {
        if (hasWriteAccess) {
            if (deviceContextPtr->IsControllerOpenForReadWrite) {
                PWM_LOG_TRACE("Controller access denied.");
                WdfRequestComplete(WdfRequest, STATUS_SHARING_VIOLATION);
                return;
            }
            deviceContextPtr->IsControllerOpenForReadWrite = true;
        }
        PWM_LOG_TRACE(
            "Controller Opened. (IsControllerOpenForReadWrite = %lu)",
            (deviceContextPtr->IsControllerOpenForReadWrite ? 1 : 0));
    }

    //
    // Allocate and fill a file object context
    //
    IMXPWM_FILE_OBJECT_CONTEXT* fileObjectContextPtr;
    {
        WDF_OBJECT_ATTRIBUTES wdfObjectAttributes;
        WDF_OBJECT_ATTRIBUTES_INIT_CONTEXT_TYPE(
            &wdfObjectAttributes,
            IMXPWM_FILE_OBJECT_CONTEXT);

        void* contextPtr;
        NTSTATUS status = WdfObjectAllocateContext(
                WdfFileObject,
                &wdfObjectAttributes,
                &contextPtr);
        if (!NT_SUCCESS(status)) {
            IMXPWM_LOG_ERROR(
                "WdfObjectAllocateContext(...) failed. (status = %!STATUS!)",
                status);
            WdfRequestComplete(WdfRequest, status);
            return;
        }

        fileObjectContextPtr =
            static_cast<IMXPWM_FILE_OBJECT_CONTEXT*>(contextPtr);

        NT_ASSERT(fileObjectContextPtr != nullptr);
        fileObjectContextPtr->IsPinInterface = isPinInterface;
        fileObjectContextPtr->IsOpenForWrite = hasWriteAccess;
        fileObjectContextPtr->PinNumber = pinNumber;
    }
    ```

- 在 EVT_WDF_FILE_CLOSE / EVT_WDF_FILE_CLEANUP，驱动程序应保持控制器/pin 状态完整性。 

  如果文件对象属于该控制器/pin 打开进行写入的控制器/pin，然后控制器/pin 重置为默认状态或取消标记该控制器/插针打开以进行写入 (是打开的-写 = false)。

  此示例实现必要的锁定逻辑来处理并发文件关闭请求未一个 EVT_WDF_DEVICE_FILE_CLOSE 处理程序的上述的访问验证步骤。
  ```cpp
  EVT_WDF_DEVICE_FILE_CLOSE PwmEvtFileClose;

  VOID
  PwmEvtFileClose (
      WDFFILEOBJECT WdfFileObject
      )
  {
      WDFDEVICE wdfDevice = WdfFileObjectGetDevice(WdfFileObject);
      PWM_DEVICE_CONTEXT* deviceContextPtr = PwmGetDeviceContext(wdfDevice);
      PWM_FILE_OBJECT_CONTEXT* fileObjectContextPtr = PwmGetFileObjectContext(WdfFileObject);

      if (fileObjectContextPtr->IsPinInterface) {
          if (fileObjectContextPtr->IsOpenForReadWrite) {
              const ULONG pinNumber = fileObjectContextPtr->PinNumber;

              NTSTATUS status = PwmResetPinDefaults(deviceContextPtr, pinNumber);
              if (!NT_SUCCESS(status)) {
                  PWM_LOG_ERROR(
                      "PwmResetPinDefaults(...) failed. "
                      "(pinNumber = %lu, status = %!STATUS!)",
                      pinNumber,
                      status);
                  //
                  // HW Error Recovery
                  //
              }

              NT_ASSERT(deviceContextPtr->Pins[pinNumber].IsOpenForReadWrite);
              deviceContextPtr->Pins[pinNumber].IsOpenForReadWrite = false;
          }

          PWM_LOG_TRACE("Pin%lu Closed.", fileObjectContextPtr->PinNumber);

      } else {
          if (fileObjectContextPtr->IsOpenForReadWrite) {
              NTSTATUS status = PwmResetControllerDefaults(deviceContextPtr);
              if (!NT_SUCCESS(status)) {
                  IMXPWM_LOG_ERROR(
                      "PwmResetControllerDefaults(...) failed. (status = %!STATUS!)",
                      status);
                  //
                  // HW Error Recovery
                  //  
              }

              NT_ASSERT(deviceContextPtr->IsControllerOpenForReadWrite);
              deviceContextPtr->IsControllerOpenForReadWrite = false;
          }

          PWM_LOG_TRACE("Controller Closed.");
      }
  }
  ```
  ## <a name="pwm-ioctl-requests"></a>PWM IOCTL 请求

PWM IOCTL 请求发送的应用程序或另一个驱动程序，并且控制器或特定 pin 的目标。

**控制器 Ioctl**

-    [**IOCTL_PWM_CONTROLLER_GET_ACTUAL_PERIOD**](https://docs.microsoft.com/windows/desktop/api/pwm/ni-pwm-ioctl_pwm_controller_get_actual_period) 
-    [**IOCTL_PWM_CONTROLLER_GET_INFO**](https://docs.microsoft.com/windows/desktop/api/pwm/ni-pwm-ioctl_pwm_controller_get_info) 
-    [**IOCTL_PWM_CONTROLLER_SET_DESIRED_PERIOD**](https://docs.microsoft.com/windows/desktop/api/pwm/ni-pwm-ioctl_pwm_controller_set_desired_period)


**Pin Ioctl**

-    [**IOCTL_PWM_PIN_GET_ACTIVE_DUTY_CYCLE_PERCENTAGE**](https://docs.microsoft.com/windows/desktop/api/pwm/ni-pwm-ioctl_pwm_pin_get_active_duty_cycle_percentage)
-    [**IOCTL_PWM_PIN_SET_ACTIVE_DUTY_CYCLE_PERCENTAGE**](https://docs.microsoft.com/windows/desktop/api/pwm/ni-pwm-ioctl_pwm_pin_set_active_duty_cycle_percentage)
-    [**IOCTL_PWM_PIN_GET_POLARITY**](https://docs.microsoft.com/windows/desktop/api/pwm/ni-pwm-ioctl_pwm_pin_get_polarity)
-    [**IOCTL_PWM_PIN_SET_POLARITY**](https://docs.microsoft.com/windows/desktop/api/pwm/ni-pwm-ioctl_pwm_pin_set_polarity)
-    [**IOCTL_PWM_PIN_START**](https://docs.microsoft.com/windows/desktop/api/pwm/ni-pwm-ioctl_pwm_pin_start)
-    [**IOCTL_PWM_PIN_STOP**](https://docs.microsoft.com/windows/desktop/api/pwm/ni-pwm-ioctl_pwm_pin_stop)
-    [**IOCTL_PWM_PIN_IS_STARTED**](https://docs.microsoft.com/windows/desktop/api/pwm/ni-pwm-ioctl_pwm_pin_is_started)    

对于每个 IOCTL 请求，PWM drivr 必须验证以下： 

1. 请求的操作 （IOCTL 代码） 是有效的请求关联的文件对象。 

2. 请求输入和输出缓冲区，并确保它们至少是最小值的预期大小。 

3. 在当前控制器/pin 状态请求的操作的有效性。 

4. 单个输入参数的有效性。 例如： 所需的期为零是 IOCTL_PWM_CONTROLLER_SET_DESIRED_PERIOD 的无效参数。 

### <a name="ioctl-completion-status-codes"></a>IOCTL 完成状态代码 

PWM 驱动程序必须完成 IOCTL 请求与相应的状态代码。 以下是常见的完成状态代码。 一般情况下，设置包含已设置的值的属性 IOCTL 应始终成功。 一个针对示例中，将完全相同的周期设置已设置，停止已停止的 pin、 已设置的设置极性等。 

**STATUS_NOT_SUPPORTED** 

请求的 IOCTL 操作未实现或支持。 例如，一些控制器可能不支持在这种情况下 IOCTL_PWM_PIN_SET_POLARITY 应实现，但对于非默认极性因 STATUS_NOT_SUPPORTED 中设置输出信号极性。 

**STATUS_INVALID_DEVICE_REQUEST** 

IOCTL 请求发送到错误的目标。 例如，控制器 IOCTL 请求已发送使用 pin 的文件句柄。 

**STATUS_BUFFER_TOO_SMALL** 

输入或输出缓冲区大小小于处理请求的最小所需的缓冲区大小。 使用 WdfRequestRetrieveInputBuffer 或 WdfRequestRetrieveOutputBuffer 检索并验证输入和输出缓冲区的 WDF 驱动程序可以返回原样及其相应的错误状态。 与所有 Ioctl 都输入和 / 或输出缓冲区为其定义具有相应的结构，描述该缓冲区，其中都输入和输出的结构名称具有*分别都输入和 _OUTPUT 后缀。输入的缓冲区的最小大小是 sizeof (PWM*<em>*输入) 时输出缓冲区最小大小是 sizeof (PWM*</em>_OUTPUT)。 

IOCTL 代码 | 描述|
---|---|
|IOCTL_PWM_CONTROLLER_GET_ACTUAL_PERIOD | 检索 Pulse 宽度调整 (PWM) 控制器的有效输出信号期间，根据它将在其输出通道测量值。 返回一个 PWM_CONTROLLER_GET_ACTUAL_PERIOD_OUTPUT 值。 Irp-> IoStatus.Status 设置为以下列表中的值之一。 <ul><li>STATUS_SUCCESS</li><li>STATUS_NOT_SUPPORTED</li><li>STATUS_INVALID_DEVICE_REQUEST<li>STATUS_BUFFER_TOO_SMALL</li></ul>|
| IOCTL_PWM_CONTROLLER_GET_INFO| 检索有关 Pulse 宽度调整 (PWM) 控制器的信息。 初始化控制器后，此信息不会更改。 <p>调用方应传入具有完全 PWM_CONTROLLER_INFO 结构的大小的输出缓冲区。 该驱动程序来推断从请求输出缓冲区大小结构的版本。 </p><p>如果缓冲区大小小于最低版本的结构的大小，该请求是通过使用 STATUS_BUFFER_TOO_SMALL IOCTL 完成状态完成。 否则，驱动程序假定可以适合于提供的输出缓冲区和成功完成请求的最高结构版本。 </p><p>较新的 PWM_CONTROLLER_INFO 版本具有的最大的以前版本的字节大小</p>Irp-> IoStatus.Status 设置为以下列表中的值之一。 <ul><li>STATUS_SUCCESS</li><li>STATUS_NOT_SUPPORTED</li><li>STATUS_INVALID_DEVICE_REQUEST<li>STATUS_BUFFER_TOO_SMALL</li></ul>|
|IOCTL_PWM_CONTROLLER_SET_DESIRED_PERIOD|设置输出信号周期的 Pulse 宽度调整 (PWM) 控制器为建议的值。 <p>PWM 控制器会尝试设置是尽可能接近到请求的值基于其功能的期限。 IOCTL 输出作为返回有效期间。 更高版本可以通过使用 IOCTL_PWM_CONTROLLER_GET_ACTUAL_PERIOD 检索它。</p><p>所需时间段必须大于零 (0) 且控制器支持范围的时间段内。 也就是说，它必须是范围的 MinimumPeriod 和 MaximumPeriod，非独占的这可以通过使用 IOCTL_PWM_CONTROLLER_GET_INFO 检索中。 </p>Irp-> IoStatus.Status 设置为以下列表中的值之一。 <ul><li>STATUS_SUCCESS</li><li>STATUS_NOT_SUPPORTED</li><li>STATUS_INVALID_DEVICE_REQUEST<li>STATUS_INVALID_PARAMETER</li><li>STATUS_BUFFER_TOO_SMALL</li></ul>|
|IOCTL_PWM_PIN_GET_ACTIVE_DUTY_CYCLE_PERCENTAGE| 检索当前占空比循环 pin 或通道的百分比。 控制代码作为 PWM_PIN_GET_ACTIVE_DUTY_CYCLE_PERCENTAGE_OUTPUT 结构返回百分比。<p>Irp-> IoStatus.Status 设置为以下列表中的值之一。</p><ul><li>STATUS_SUCCESS</li><li>STATUS_NOT_SUPPORTED</li><li>STATUS_INVALID_DEVICE_REQUEST<li>STATUS_BUFFER_TOO_SMALL</li></ul>|
|IOCTL_PWM_PIN_SET_ACTIVE_DUTY_CYCLE_PERCENTAGE|设置控制器 pin 或通道所需的值班周期百分比值。 控制代码作为 PWM_PIN_SET_ACTIVE_DUTY_CYCLE_PERCENTAGE_INPUT 结构指定的百分比。<p>Irp-> IoStatus.Status 设置为以下列表中的值之一。</p> <ul><li>STATUS_SUCCESS</li><li>STATUS_NOT_SUPPORTED</li><li>STATUS_INVALID_DEVICE_REQUEST<li>STATUS_BUFFER_TOO_SMALL</li></ul>|
|IOCTL_PWM_PIN_GET_POLARITY| 检索当前的 pin 或通道信号极性。 控制代码获取信号极性作为 PWM_PIN_GET_POLARITY_OUTPUT 结构。 信号极性是 Active 高或低电平 PWM_POLARITY 枚举中定义。<p>Irp-> IoStatus.Status 设置为以下列表中的值之一。</p> <ul><li>STATUS_SUCCESS</li><li>STATUS_NOT_SUPPORTED</li><li>STATUS_INVALID_DEVICE_REQUEST<li>STATUS_BUFFER_TOO_SMALL</li></ul>|
|IOCTL_PWM_PIN_SET_POLARITY| 设置 pin 或通道的信号极性。 控制代码设置信号极性基于 PWM_PIN_SET_POLARITY_INPUT 结构。 信号极性是 Active 高或低电平 PWM_POLARITY 枚举中定义。 <p>当停止 pin 时，才允许更改极性。 您可以告知 pin 已停止使用 IOCTL_PWM_PIN_IS_STARTED 控制代码。 如果请求的极性是不同于当前的 pin 极性 pin 已停止，该请求是已完成，但 STATUS_INVALID_DEVICE_STATE 值。</p><p>更改时，启动 pin 的极性，则可能会导致某些 Pulse 宽度调整 (PWM) 控制器上问题。 如果你想要更改极性，首先停止 pin、 更改极性，并启动 pin。</p><p>Irp-> IoStatus.Status 设置为以下列表中的值之一。</p><ul><li>STATUS_SUCCESS</li><li>STATUS_NOT_SUPPORTED</li><li>STATUS_INVALID_DEVICE_REQUEST<li>STATUS_INVALID_PARAMETER</li><li>STATUS_BUFFER_TOO_SMALL</li></ul>|
|IOCTL_PWM_PIN_START|Pin 或通道上启动 Pulse 宽度调整 (PWM) 信号的生成。 若要检查是否已启动 pin，请使用 IOCTL_PWM_PIN_IS_STARTED。<p>发出此 IOCTL pin 或已启动的通道上没有影响，但未成功。</p><p>Irp-> IoStatus.Status 设置为以下列表中的值之一。</p>><ul><li>STATUS_SUCCESS</li><li>STATUS_NOT_SUPPORTED</li><li>STATUS_INVALID_DEVICE_REQUEST<li>STATUS_BUFFER_TOO_SMALL</li></ul>|
|IOCTL_PWM_PIN_STOP|Pin 或通道上停止生成 Pulse 宽度调整 (PWM) 信号。 若要检查是否已启动 pin，请使用 IOCTL_PWM_PIN_IS_STARTED。<p>发出此 IOCTL pin 或已停止的通道上没有影响，但未成功。</p><p>Irp-> IoStatus.Status 设置为以下列表中的值之一。</p><ul><li>STATUS_SUCCESS</li><li>STATUS_NOT_SUPPORTED</li><li>STATUS_INVALID_DEVICE_REQUEST<li>STATUS_BUFFER_TOO_SMALL</li></ul>|
|IOCTL_PWM_PIN_IS_STARTED|检索的 pin 或通道的信号生成的状态。 启动或停止为 PWM_PIN_IS_STARTED_OUTPUT 结构，每个 pin 具有的状态。 已启动的状态具有布尔值为 true。 已停止的状态为 false。 <p>默认情况下，pin 打开时已停止，并返回为已停止状态时将其关闭，关闭或释放。</p><p>Irp-> IoStatus.Status 设置为以下列表中的值之一。</p><ul><li>STATUS_SUCCESS</li><li>STATUS_NOT_SUPPORTED</li><li>STATUS_INVALID_DEVICE_REQUEST<li>STATUS_BUFFER_TOO_SMALL</li></ul>|


