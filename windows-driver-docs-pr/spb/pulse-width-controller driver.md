---
title: SoC 上 PWM 模块的 PWM 驱动程序
description: PWM 控制器是 SoC 和内存映射到 SoC 地址空间的一部分。 编写一个内核模式驱动程序，该驱动程序操作 PWM 寄存器并提供对应用程序的访问。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d5eb78c32120612290775c52007845830827c467
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96835415"
---
# <a name="pwm-driver-for-an-on-soc-pwm-module"></a>SoC 上 PWM 模块的 PWM 驱动程序
若要访问脉冲宽度调制 (PWM) 控制器，该控制器是 SoC 和内存映射到 SoC 地址空间的一部分，则需要编写一个内核模式驱动程序。 驱动程序必须注册 PWM 控制器的设备类接口，以便 UWP 应用可以通过在 Pwm 命名空间中定义的 PWM WinRT Api 访问系统公开的 PWM 设备。 

**注意**    如果已通过 I <sup>2</sup>C、SPI 或 UART 控制器使用外接程序 PWM 模块，则可以使用 [**PWM**](/uwp/api/windows.devices.pwm) 和 [**PWM**](/uwp/api/windows.devices.pwm.provider) 命名空间中定义的 api 从 UWP 应用程序访问该模块。 

PWM 设备抽象成单个控制器和一个或多个 pin。 控制控制器或 pin 是通过 PWM 定义的 IOCTLs 来完成的。 例如，LCD 显示驱动程序将此类请求发送到 PWM 驱动程序，以控制 LCD 背光级别。 

多控制器和多通道 PWM 信号生成，其中包含可配置的期间、极性和责任周期，可用于执行以下任务： 

-   驱动伺服电动机。 
-   推动一种负载，如 LED 或直流电拉绒马达。 
-   生成模拟信号。 
-   生成精确时钟。 

本主题介绍、 

-   如何对系统公开的 PWM 设备启用 UWP 访问。 

-   如何处理由 Win32 应用程序或第三方内核模式驱动程序发送的 PWM IOCTL 请求。

**目标受众**

-   使用 SoC PWM 控制器开发系统的 Oem 和 Ihv。 

**上次更新时间**

-   2017 年 8 月

**Windows 版本**

-   Windows 10 版本

**重要的 API**

-   [PWM IOCTLs](/windows/desktop/DevIO/pwm-api)

## <a name="about-pwm"></a>关于 PWM
PWM 介绍了用于生成具有调制脉冲宽度的矩形脉冲的基本方法，这会导致波形的平均值变体。  

可以通过2个参数对 PWM 波形进行分类：波形期间 (T) 和岗位循环。 波形频率 (f) 是波形句号 f = 1/T 的倒数。 "责任周期" 描述 "开" 或 "活动" 时间相对于时间间隔或 "时间段" 的比例;低责任周期对应于平均的低输出能力，因为在大多数情况下电源已关闭。 关税周期以百分比表示，其中100% 处于完全关闭状态，0% 表示完全关闭，50% 为 "活动" 50%。

![驱动程序](images/pwm.png)


## <a name="accessing-the-system-exposed-pwm-controller-and-pins"></a>访问系统公开的 PWM 控制器和 pin

PWM 驱动程序必须注册  
GUID_DEVINTERFACE_PWM_CONTROLLER 为公开和访问 PWM 设备的设备接口 GUID。 

```cpp
// {60824B4C-EED1-4C9C-B49C-1B961461A819} 

DEFINE_GUID(GUID_DEVINTERFACE_PWM_CONTROLLER, 0x60824b4c, 0xeed1, 0x4c9c, 0xb4, 0x9c, 0x1b, 0x96, 0x14, 0x61, 0xa8, 0x19); 

#define GUID_DEVINTERFACE_PWM_CONTROLLER_WSZ L"{60824B4C-EED1-4C9C-B49C-1B961461A819}" 
```

若要注册设备接口 GUID，驱动程序必须在 EVT_WDF_DRIVER_DEVICE_ADD 回调函数的驱动程序实现中调用 WdfDeviceCreateDeviceInterface。 注册后，系统会为控制器和 pin 分配一个符号链接。

应用程序或另一个驱动程序可以通过 PWM 定义的 IOCTLs 控制控制器或 pin。 发送 IOCTLs 之前，发送方应用程序或驱动程序必须通过指定其符号链接打开控制器和 pin 的文件句柄。 这要求驱动程序注册文件创建和关闭事件。 请参阅 (链接)  


下面是控制器的符号路径示例：
```cpp
\??\ACPI#FSCL000E#1#{60824b4c-eed1-4c9c-b49c-1b961461a819}  
```
同样，pin 的格式如下所示：路径的格式如下所示：

```cpp
<DeviceInterfaceSymbolicLinkName>\<PinNumber>
```
其中 <PinNumber> ，是要打开的 pin 的从零开始的索引。 

下面是 pin 符号路径的示例：
```cpp
\??\ACPI#FSCL000E#1#{60824b4c-eed1-4c9c-b49c-1b961461a819}\0 ; Opens pin 0 

\??\ACPI#FSCL000E#1#{60824b4c-eed1-4c9c-b49c-1b961461a819}\0001 ; Opens pin 1 with the leading 0s have no effect.
```

若要打开文件句柄，应用程序必须 (CM_Get_Device_Interface_ * ) 调用 Configuration Manager Api。 

打开文件句柄后，应用程序可以通过调用 DeviceIoControl 函数发送这些请求。 请参阅 PWM 部分。



驱动程序应使用提供的 PWM 支持例程 PwmParsePinPath 来分析和验证 pin 路径并提取 pin 号。 

## <a name="setting-device-interface-properties"></a>设置设备接口属性

若要从 UWP 应用中使用 PWM WinRT Api，必须设置这些 [设备接口属性](/previous-versions/ff541409(v=vs.85)) 。

-   [DEVPKEY_DeviceInterface_Restricted](../install/devpkey-deviceinterface-restricted.md) 

    根据当前 UWP 设备访问模型，需要将 "受限制的设备接口" 属性设置为 "FALSE"，以使 UWP 应用能够访问 PWM 设备接口。   

-    (链接 DEVPKEY_DeviceInterface_SchematicName???) 

    若要使用 PwmController (FriendlyName) factory 方法，需要将示意名称分配给静态连接的 PWM 设备的 PWM 设备接口。 示意性名称是系统设计示意图中为 PWM 设备指定的名称，例如 (PWM0，PWM_1，et。) 。 假设示意名称在整个系统中是唯一的，但这不是强制性的。 至少，不应有2个具有相同示意性名称的 PWM 设备，否则，WinRT PWM PwmController GetDeviceSelector (FriendlyName) 行为将是不确定的。 

可以通过以下两种方式之一设置属性：

1. 使用 PWM 驱动程序的 INF 文件

   使用 **AddProperty** 指令设置设备属性。 INF 文件应该允许为一个或多个 PWM 设备实例的同一属性设置不同的值。 下面是设置 DEVPKEY_DeviceInterface_Restricted 的示例。
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
    并非所有设计都具有与向 UWP 公开 PWM 设备相同的策略。 例如，策略可能是允许 UWP 访问 PWM 设备实例的子集。 若要公开 PWM 设备的子集或将不同的属性值分配给一个或多个 PWM 设备实例，需要为每个 PWM 设备实例提供不同的硬件 ID，并根据策略有选择性地匹配 INF 部分。

    请考虑使用基于 SoC 的设计，其中有四个相同的 PWM 设备实例 () 名为 PWM0,..., PWM3 的 "ACPI 分配硬件 ID" 的，其中其 ACPI 分配的硬件 (_HID ID) 为 FSCL00E0，其唯一 ID (_UID) 为 0,..., 3。 向 UWP 公开所有 PWM 设备将需要 INF 部分来设置要与硬件 ID 匹配的 DEVPKEY_DeviceInterface_Restricted ACPI\FSCL00E0。 

    这种设置属性的方法不需要对驱动程序代码进行任何更改。 这是一个更简单的选项，因为服务 INF 文件比驱动程序二进制文件更容易。 权衡是，这种方法需要为每个设计定制一个 INF 文件。 


2.  在 PWM 驱动程序中以编程方式 

    PWM 驱动程序可以在创建和发布 PWM 设备接口后，调用 IoSetDeviceInterfacePropertyData，在其 EVT_WDF_DRIVER_DEVICE_ADD 实现中设置设备接口属性。 驱动程序负责确定要分配的值和设备属性。 该信息通常存储在系统 ACPI 中，用于基于 SoC 的设计。 每个设备接口属性的值可在每个 ACPI 设备节点 _DSD 方法中指定为设备属性。 驱动程序必须从 ACPI 查询 _DSD，分析设备属性数据，提取每个属性的值，并为其分配设备接口。 

    以编程方式设置这些属性会使驱动程序及其 INF 文件在设计上是可移植的，因此 Bsp 的是在 ACPI DSDT 中定义每个 PWM 设备节点的唯一更改。 但是，读取和分析 ACPI 二进制文件块是一项单调的工作，并且需要大量代码，这可能会容易出现错误和漏洞，导致出现更大的错误。 

## <a name="handling-file-openclose-events"></a>处理文件打开/关闭事件

PWM 驱动程序需要通过实现 EVT_WDF_DEVICE_FILE_CREATE 和 EVT_WDF_FILE_CLEANUP/EVT_WDF_FILE_CLOSE 回调函数来注册文件创建和关闭事件。 在实现中，驱动程序必须执行以下任务：

1.  确定创建请求是用于控制器还是用于 pin。 
2.  如果请求用于 pin，则驱动程序必须分析和验证创建 pin 请求的 pin 路径，并确保请求的 pin 号在控制器边界内。 
3.  授予或拒绝对控制器和 pin 创建请求的访问权限。 
4.  按定义良好的状态机维护控制器和 pin 状态完整性。 

在前面的任务集中，可以在 EVT_WDF_DEVICE_FILE_CREATE 中执行第二次验证任务，如下所示：

1. 如果与请求文件对象关联的文件名为 null，则完成请求并 STATUS_INVALID_DEVICE_REQUEST。 

2. 如果与请求文件对象关联的文件名为空字符串，则这是控制器创建请求，否则为 pin 创建请求。 

3. 如果这是 pin 创建请求，则： 

    1. 根据格式分析 pin 路径 \<DecimalName> ，并通过调用 PwmParsePinPath 来提取 pin 号。 

    2. 如果解析和验证 pin 路径失败，请完成 STATUS_NO_SUCH_FILE 的请求。 

    3. 如果 pin 号大于或等于控制器 pin 计数，请完成请求并 STATUS_NO_SUCH_FILE。 请注意，pin 号是从零开始的索引。 

    4. 否则，请继续处理 EVT_WDF_DEVICE_FILE_CREATE。 

下面是一个示例代码，它为 EVT_WDF_DEVICE_FILE_CREATE 处理程序实现前面提到的验证步骤： 

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

控制器和 pin 的共享模型遵循多个读取器（单个写入器模式）。 可以打开控制器/pin，使其可供多个调用方读取，但只有一个调用方可以打开该控制器/pin 以便一次写入。 

当打开文件句柄时，可以结合使用所需的访问和共享访问标志来实现该模型。 DDI 共享模式将在仅使用所需访问规范来控制访问权限的情况下，获取更简单的共享语义。 共享访问规范不会在共享模型中扮演任何角色，如果在打开控制器或 pin 时指定，则不遵循该规范。  

在 EVT_WDF_DEVICE_FILE_CREATE 中，应根据控制器/pin 状态提取并验证创建请求所需的访问权限和共享访问权限，如下所示： 

1. 如果共享访问不是0，则拒绝访问，并 STATUS_SHARING_VIOLATION 的完成请求。 

2. 如果所需的访问权限为只读，则授予访问权限并继续处理 EVT_WDF_DEVICE_FILE_CREATE。 

3. 如果所需的访问权限用于写入，则： 

如果控制器/pin 已打开以进行写入，则拒绝访问，并使用 STATUS_SHARING_VIOLATION 完成请求，否则授予访问权限，将控制器或 pin 标记为打开以供写入并继续处理 EVT_WDF_DEVICE_FILE_CREATE。 

下面是一个示例，演示如何从创建请求中提取所需的访问权限和共享访问权限： 

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

控制器和 pin 具有父子展示。 若要打开 pin，必须首先打开其父控制器。 另一种方法是查看 pin 作为独立实体，其中其父控制器仅向 pin 提供一项服务，这是为该控制器上包含的所有 pin 设置全局 PWM 时间段。 

下面是一些示例方案： 

- 单进程访问： 

    -   进程 A 可以打开该 pin，设置其职责周期，使用控制器默认时间段启动它，稍后打开控制器并根据需要设置时间段。 如果应用程序的默认时间段是正常的，则不需要打开控制器。 

    -   一个进程可以有多个线程，其中每个线程控制同一个控制器下的不同 pin。 

- 多进程访问： 

    -   命令行实用工具可以打开具有只读访问权限的控制器，目的是为了向控制台显示信息。 同时，后台 UWP 任务可以打开控制器以进行写入，并使用单个 pin 控制某些 LED。 

    -   一种内核模式显示驱动程序，通过 Pin0 控制 LCD 背光，同时按住控制器以写入和锁定 PWM 期间。 同时，Win32 服务使用显示驱动程序设置的 PWM 时间段，并使用 Pin1 使某些 LED 向用户传达某些状态。 

请注意，在独立于控制器的针脚之间打开和关闭控制器有一些重要的影响。 有关详细信息，请参阅状态机部分。 

## <a name="controller-and-pin-state-machines"></a>控制器和 pin 状态机

**控制器状态定义**

|状态功能|默认值|说明|
|---|---|--|
|已打开-用于写入|错误| False 指示控制器已关闭或已打开以进行读取;如果为 True，则表示它已打开以进行写入。|
|Desired-Period| MinimumPeriod| |

![控制器状态机](images/controller-state-machine.png)

下面的控制器状态机以仅限打开的-写状态为中心。 所需的期限值也将被省略，因为它不会影响可在控制器上执行的操作的类型。 请注意，只要打开的控制器被打开以进行写入的调用方关闭，控制器就会重置为默认 (所需的) 默认时间段。

**固定状态定义**


|    状态功能    | 默认值 |                                                   说明                                                    |
|---------------------|---------------|------------------------------------------------------------------------------------------------------------------|
| 已打开-用于写入 |     错误     | False 表示关闭或打开以进行读取;如果为 True，则表示它已打开以进行写入。 |
|  主动-周期  |       0       |                                                                                                                  |
|     Is-Started      |     错误     |                                 False 表示已停止;True 表示开始。                                 |

![Pin 状态机](images/pins-state-machine.png)

Pin 状态机的中心围绕2个状态的组合： "已打开-写入" 和 "已启动"。 其他 pin 状态（如极性和活动的工作周期）会保持不变，因为它们的值不会影响可在 pin 上执行的操作的类型。 请注意，每次打开以进行写入的 pin 都由打开它以进行写入的调用方关闭时，该 pin 会恢复其默认值 (停止、默认极性和活动的工作周期) 。 另请注意，在 Is-Started 为 true 的状态上 Set-Polarity 转换被保留，因为它在该状态下无效。

给定状态中未提及的任何转换都意味着此类转换无效或不可能，并应使用适当的错误状态完成相应的请求。 

### <a name="implementation-considerations-for-state-transitions"></a>状态转换的实现注意事项

- 在 EVT_WDF_DEVICE_FILE_CREATE 中，驱动程序应基于 "创建请求所需的访问权限"、"控制器" 或 "pin 已打开-写入" 状态来授予或拒绝访问权限，如下所示：

    如果请求具有写入所需的访问权限，并且控制器/pin 已打开以进行写入，则使用 STATUS_SHARING_VIOLATION 完成请求，否则将控制器/pin 标记为打开以写入 (打开-对于写入 = true) ，授予访问权限并继续处理。

    此示例为 EVT_WDF_DEVICE_FILE_CREATE 处理程序实现前面提到的访问验证步骤，其中省略了用于处理并发文件创建请求的必要锁定逻辑： 
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

- 在 EVT_WDF_FILE_CLOSE/EVT_WDF_FILE_CLEANUP 中，驱动程序应维护控制器/pin 状态完整性。 

  如果文件对象属于打开该控制器/pin 以进行写入的控制器/pin，则将控制器/pin 重置为默认状态，并取消打开控制器/pin 以使写入 (打开-用于写入 = false) 。

  此示例为 EVT_WDF_DEVICE_FILE_CLOSE 处理程序实现前面提到的访问验证步骤，其中省略了处理并发文件关闭请求所需的锁定逻辑。
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

PWM IOCTL 请求由应用程序或其他驱动程序发送，并以控制器或特定的 pin 为目标。

**控制器 IOCTLs**

-    [**IOCTL_PWM_CONTROLLER_GET_ACTUAL_PERIOD**](/windows/win32/api/pwm/ni-pwm-ioctl_pwm_controller_get_actual_period) 
-    [**IOCTL_PWM_CONTROLLER_GET_INFO**](/windows/win32/api/pwm/ni-pwm-ioctl_pwm_controller_get_info) 
-    [**IOCTL_PWM_CONTROLLER_SET_DESIRED_PERIOD**](/windows/win32/api/pwm/ni-pwm-ioctl_pwm_controller_set_desired_period)


**固定 IOCTLs**

-    [**IOCTL_PWM_PIN_GET_ACTIVE_DUTY_CYCLE_PERCENTAGE**](/windows/win32/api/pwm/ni-pwm-ioctl_pwm_pin_get_active_duty_cycle_percentage)
-    [**IOCTL_PWM_PIN_SET_ACTIVE_DUTY_CYCLE_PERCENTAGE**](/windows/win32/api/pwm/ni-pwm-ioctl_pwm_pin_set_active_duty_cycle_percentage)
-    [**IOCTL_PWM_PIN_GET_POLARITY**](/windows/win32/api/pwm/ni-pwm-ioctl_pwm_pin_get_polarity)
-    [**IOCTL_PWM_PIN_SET_POLARITY**](/windows/win32/api/pwm/ni-pwm-ioctl_pwm_pin_set_polarity)
-    [**IOCTL_PWM_PIN_START**](/windows/win32/api/pwm/ni-pwm-ioctl_pwm_pin_start)
-    [**IOCTL_PWM_PIN_STOP**](/windows/win32/api/pwm/ni-pwm-ioctl_pwm_pin_stop)
-    [**IOCTL_PWM_PIN_IS_STARTED**](/windows/win32/api/pwm/ni-pwm-ioctl_pwm_pin_is_started)    

对于每个 IOCTL 请求，PWM drivr 必须验证以下各项： 

1. 请求的操作 (IOCTL 代码) 对于关联的文件对象是有效的。 

2. 请求输入和输出缓冲区，并确保它们至少达到最小预期大小。 

3. 当前控制器/pin 状态中请求的操作的有效性。 

4. 单个输入参数的有效性。 例如：所需的零段是 IOCTL_PWM_CONTROLLER_SET_DESIRED_PERIOD 的无效参数。 

### <a name="ioctl-completion-status-codes"></a>IOCTL 完成状态代码 

PWM 驱动程序必须用适当的状态代码完成 IOCTL 请求。 下面是常见的完成状态代码。 通常，使用已设置的值设置属性的 IOCTL 应始终会成功。 Foe 示例，设置已经设置的完全相同的时间，停止已停止的 pin，设置已设置的极性等。 

**STATUS_NOT_SUPPORTED** 

请求的 IOCTL 操作未实现或不受支持。 例如，某些控制器可能不支持设置输出信号极性，在这种情况下 IOCTL_PWM_PIN_SET_POLARITY 应该实现但对于非默认极性 STATUS_NOT_SUPPORTED 失败。 

**STATUS_INVALID_DEVICE_REQUEST** 

IOCTL 请求已发送到错误目标。 例如，控制器 IOCTL 请求是使用 pin 文件句柄发送的。 

**STATUS_BUFFER_TOO_SMALL** 

输入或输出缓冲区的大小小于处理请求所需的最小缓冲区大小。 使用 WdfRequestRetrieveInputBuffer 或 WdfRequestRetrieveOutputBuffer 检索和验证输入和输出缓冲区的 WDF 驱动程序可以按原样返回其相应的错误状态。 所有 IOCTLs 都定义了输入和/或定义的输出缓冲区，其中包含一个描述该缓冲区的相应结构，其中输入和输出结构名称 *分别具有输入和 _OUTPUT 后缀。输入缓冲区最小大小为 sizeof (PWM*<em>*输入) 而输出缓冲区最小大小为 SIZEOF (PWM*</em>_OUTPUT) 。 

IOCTL 代码 | 描述|
---|---|
|IOCTL_PWM_CONTROLLER_GET_ACTUAL_PERIOD | 检索脉冲宽度调制 (PWM) 控制器的有效输出信号周期，因为它将在输出通道上测量。 返回 PWM_CONTROLLER_GET_ACTUAL_PERIOD_OUTPUT 值。 Irp->IoStatus 设置为以下列表中的一个值。 <ul><li>STATUS_SUCCESS</li><li>STATUS_NOT_SUPPORTED</li><li>STATUS_INVALID_DEVICE_REQUEST<li>STATUS_BUFFER_TOO_SMALL</li></ul>|
| IOCTL_PWM_CONTROLLER_GET_INFO| 检索有关脉冲宽度调制 (PWM) 控制器的信息。 此信息不会在控制器初始化后发生更改。 <p>调用方应传递大小刚好为 PWM_CONTROLLER_INFO 结构的输出缓冲区。 驱动程序从请求输出缓冲区的大小中推断出结构的版本。 </p><p>如果缓冲区大小小于最低的结构版本大小，则使用 STATUS_BUFFER_TOO_SMALL 的 IOCTL 完成状态来完成请求。 否则，驱动程序将假定可在提供的输出缓冲区中容纳的最高结构版本并成功完成请求。 </p><p>较新的 PWM_CONTROLLER_INFO 版本的字节大小大于以前版本的大小</p>Irp->IoStatus 设置为以下列表中的一个值。 <ul><li>STATUS_SUCCESS</li><li>STATUS_NOT_SUPPORTED</li><li>STATUS_INVALID_DEVICE_REQUEST<li>STATUS_BUFFER_TOO_SMALL</li></ul>|
|IOCTL_PWM_CONTROLLER_SET_DESIRED_PERIOD|将脉冲宽度调制 (PWM) 控制器的输出信号周期设置为建议的值。 <p>PWM 控制器尝试根据其功能将时间间隔设置为尽可能靠近请求的值。 有效期作为 IOCTL 输出返回。 稍后可以使用 IOCTL_PWM_CONTROLLER_GET_ACTUAL_PERIOD 来检索它。</p><p>所需的时间段必须大于零 (0) 和控制器支持的时间范围。 也就是说，它必须在 MinimumPeriod 和 MaximumPeriod （含）范围内，可以使用 IOCTL_PWM_CONTROLLER_GET_INFO 来检索。 </p>Irp->IoStatus 设置为以下列表中的一个值。 <ul><li>STATUS_SUCCESS</li><li>STATUS_NOT_SUPPORTED</li><li>STATUS_INVALID_DEVICE_REQUEST<li>STATUS_INVALID_PARAMETER</li><li>STATUS_BUFFER_TOO_SMALL</li></ul>|
|IOCTL_PWM_PIN_GET_ACTIVE_DUTY_CYCLE_PERCENTAGE| 检索 pin 或通道的当前关税周期百分比。 控制代码以 PWM_PIN_GET_ACTIVE_DUTY_CYCLE_PERCENTAGE_OUTPUT 结构的形式返回百分比。<p>Irp->IoStatus 设置为以下列表中的一个值。</p><ul><li>STATUS_SUCCESS</li><li>STATUS_NOT_SUPPORTED</li><li>STATUS_INVALID_DEVICE_REQUEST<li>STATUS_BUFFER_TOO_SMALL</li></ul>|
|IOCTL_PWM_PIN_SET_ACTIVE_DUTY_CYCLE_PERCENTAGE|为控制器 pin 或通道设置所需的关税周期百分比值。 控制代码将百分比指定为 PWM_PIN_SET_ACTIVE_DUTY_CYCLE_PERCENTAGE_INPUT 结构。<p>Irp->IoStatus 设置为以下列表中的一个值。</p> <ul><li>STATUS_SUCCESS</li><li>STATUS_NOT_SUPPORTED</li><li>STATUS_INVALID_DEVICE_REQUEST<li>STATUS_BUFFER_TOO_SMALL</li></ul>|
|IOCTL_PWM_PIN_GET_POLARITY| 检索 pin 或通道的当前信号极性。 控制代码将信号极性获取为 PWM_PIN_GET_POLARITY_OUTPUT 结构。 如 PWM_POLARITY 枚举中定义的那样，信号极性为活动的高或低。<p>Irp->IoStatus 设置为以下列表中的一个值。</p> <ul><li>STATUS_SUCCESS</li><li>STATUS_NOT_SUPPORTED</li><li>STATUS_INVALID_DEVICE_REQUEST<li>STATUS_BUFFER_TOO_SMALL</li></ul>|
|IOCTL_PWM_PIN_SET_POLARITY| 设置 pin 或通道的信号极性。 控制代码根据 PWM_PIN_SET_POLARITY_INPUT 结构设置信号极性。 信号极性为活动高或活动低，如 PWM_POLARITY 枚举中所定义。 <p>仅当 pin 停止时才允许更改极性。 可以通过使用 IOCTL_PWM_PIN_IS_STARTED 控制代码来确定是否停止了 pin。 如果 pin 已停止，并且请求的极性不同于当前的 pin 极性，则请求将以 STATUS_INVALID_DEVICE_STATE 值结束。</p><p>在启动 pin 的同时更改极性可能导致某些脉冲宽度调制 (PWM) 控制器出现故障。 如果要更改极性，请先停止 pin，更改极性，然后启动 pin。</p><p>Irp->IoStatus 设置为以下列表中的一个值。</p><ul><li>STATUS_SUCCESS</li><li>STATUS_NOT_SUPPORTED</li><li>STATUS_INVALID_DEVICE_REQUEST<li>STATUS_INVALID_PARAMETER</li><li>STATUS_BUFFER_TOO_SMALL</li></ul>|
|IOCTL_PWM_PIN_START|开始在 pin 或通道上生成脉冲宽度调制 (PWM) 信号。 若要检查是否已启动 pin，请使用 IOCTL_PWM_PIN_IS_STARTED。<p>在已启动的 pin 或通道上发出此 IOCTL 不起作用，但会成功。</p><p>Irp->IoStatus 设置为以下列表中的一个值。</p>><ul><li>STATUS_SUCCESS</li><li>STATUS_NOT_SUPPORTED</li><li>STATUS_INVALID_DEVICE_REQUEST<li>STATUS_BUFFER_TOO_SMALL</li></ul>|
|IOCTL_PWM_PIN_STOP|停止生成脉冲宽度调制 (PWM) 插针或通道上的信号。 若要检查是否已启动 pin，请使用 IOCTL_PWM_PIN_IS_STARTED。<p>在已停止的 pin 或通道上发出此 IOCTL 不起作用，但会成功。</p><p>Irp->IoStatus 设置为以下列表中的一个值。</p><ul><li>STATUS_SUCCESS</li><li>STATUS_NOT_SUPPORTED</li><li>STATUS_INVALID_DEVICE_REQUEST<li>STATUS_BUFFER_TOO_SMALL</li></ul>|
|IOCTL_PWM_PIN_IS_STARTED|检索 pin 或通道生成信号的状态。 每个 pin 的状态均为 "已启动" 或 "已停止" 作为 PWM_PIN_IS_STARTED_OUTPUT 结构。 "已启动" 状态的布尔值为 true。 停止状态为 false。 <p>默认情况下，pin 会在打开时停止，并在关闭或释放时返回到停止状态。</p><p>Irp->IoStatus 设置为以下列表中的一个值。</p><ul><li>STATUS_SUCCESS</li><li>STATUS_NOT_SUPPORTED</li><li>STATUS_INVALID_DEVICE_REQUEST<li>STATUS_BUFFER_TOO_SMALL</li></ul>|
