---
description: 描述 (UDE) 类扩展和客户端驱动程序必须为其附加的设备执行的客户端驱动程序的 USB 设备仿真的行为。
title: 编写 UDE 客户端驱动程序
ms.date: 01/07/2019
ms.localizationpriority: medium
ms.openlocfilehash: 2fc703a2199c30b0a49bb691b54ae845bf41bc7e
ms.sourcegitcommit: e6d80e33042e15d7f2b2d9868d25d07b927c86a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/05/2020
ms.locfileid: "91733021"
---
# <a name="write-a-ude-client-driver"></a>编写 UDE 客户端驱动程序

**摘要**

- 类扩展和客户端驱动程序使用的 UDE 对象和句柄。
- 使用功能创建模拟主机控制器以查询控制器功能并重置控制器。
- 创建虚拟 USB 设备，通过终结点设置电源管理和数据传输。

**适用对象：**

- Windows 10

**上次更新时间：**

- 2015 年 11 月

**重要的 API**

- [模拟 USB 主控制器驱动程序编程参考](/previous-versions/windows/hardware/drivers/mt628025(v=vs.85))

描述 (UDE) 类扩展和客户端驱动程序必须为其附加的设备执行的客户端驱动程序的 USB 设备仿真的行为。 它提供有关类驱动程序和类扩展如何通过一组例程和回调函数与每个进行通信的信息。 它还描述了客户端驱动程序应该实现的功能。

## <a name="before-you-begin"></a>准备阶段

-  (WDK) 你的开发计算机上[安装](../download-the-wdk.md)最新的 Windows 驱动程序工具包。 工具包具有编写 UDE 客户端驱动程序所需的头文件和库，具体而言，你将需要：
  - 存根库， (Udecxstub) 。 库转换客户端驱动程序发出的调用，并将其传递给 UdeCx。
  - 标头文件 Udecx。
- 在目标计算机上安装 Windows 10。
- 熟悉 UDE。 请参阅 [体系结构： USB 设备仿真 (UDE) ](usb-emulated-device--ude--architecture.md)。
- 熟悉 Windows Driver Foundation (WDF) 。 建议读物： [开发带有 Windows Driver Foundation 的驱动程序]( https://go.microsoft.com/fwlink/p/?LinkId=691676)（由 "Orwick" 和 "专家 Smith" 编写）。

## <a name="ude-objects-and-handles"></a>UDE 对象和句柄

UDE 类扩展和客户端驱动程序使用表示仿真主机控制器和虚拟设备的特定 WDF 对象，其中包括用于在设备和主机之间传输数据的终结点和 URBs。 客户端驱动程序请求创建对象，并通过类扩展来管理对象的生存期。

- ** (WDFDEVICE 的仿真主机控制器对象) **

    表示仿真主机控制器，是 UDE 类扩展和客户端驱动程序之间的主句柄。

- **UDE 设备对象 (UDECXUSBDEVICE) **

    表示连接到仿真主机控制器上某个端口的虚拟 USB 设备。

- **UDE 终结点对象 (UDECXUSBENDPOINT) **

    表示 USB 设备的顺序数据管道。 用于接收用于在终结点上发送或接收数据的软件请求。

## <a name="initialize-the-emulated-host-controller"></a>初始化仿真主机控制器

下面是客户端驱动程序检索仿真主机控制器的 WDFDEVICE 句柄的序列的摘要。 建议驱动程序在其 [*EvtDriverDeviceAdd*](/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add) 回调函数中执行这些任务。

1. 通过将引用传递给框架传递的[WDFDEVICE \_ INIT](../wdf/wdfdevice_init.md)调用[**UdecxInitializeWdfDeviceInit**](/windows-hardware/drivers/ddi/udecxwdfdevice/nf-udecxwdfdevice-udecxinitializewdfdeviceinit) 。
2. 将 [WDFDEVICE \_ INIT](../wdf/wdfdevice_init.md) 结构初始化为安装程序信息，使此设备与其他 USB 主机控制器类似。 例如，分配 FDO 名称和符号链接，将设备接口注册为 Microsoft 提供的 GUID \_ DEVINTERFACE \_ USB \_ 主机 \_ 控制器 GUID 作为设备接口 guid，以便应用程序可以打开设备的句柄。
3. 调用 [**WdfDeviceCreate**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate) 以创建框架设备对象。
4. 调用 [**UdecxWdfDeviceAddUsbDeviceEmulation**](/windows-hardware/drivers/ddi/udecxwdfdevice/nf-udecxwdfdevice-udecxwdfdeviceaddusbdeviceemulation) 并注册客户端驱动程序的回调函数。

    下面是与宿主控制器对象关联的回调函数，由 UDE 类扩展调用。 这些函数必须由客户端驱动程序实现。

    [*.EVT \_ UDECX \_ WDF \_ 设备 \_ 查询 \_ USB \_ 功能*](/windows-hardware/drivers/ddi/udecxwdfdevice/nc-udecxwdfdevice-evt_udecx_wdf_device_query_usb_capability)  
    确定主机控制器支持的、客户端驱动程序必须向类扩展报告的功能。

    [*.EVT \_ UDECX \_ WDF \_ 设备 \_ 重置*](/windows-hardware/drivers/ddi/udecxwdfdevice/nc-udecxwdfdevice-evt_udecx_wdf_device_reset)  
    可选。 重置主机控制器和/或连接的设备。

    ```cpp

    EVT_WDF_DRIVER_DEVICE_ADD                 Controller_WdfEvtDeviceAdd;

    #define BASE_DEVICE_NAME                  L"\\Device\\USBFDO-"
    #define BASE_SYMBOLIC_LINK_NAME           L"\\DosDevices\\HCD"

    #define DeviceNameSize                    sizeof(BASE_DEVICE_NAME)+MAX_SUFFIX_SIZE
    #define SymLinkNameSize                   sizeof(BASE_SYMBOLIC_LINK_NAME)+MAX_SUFFIX_SIZE

    NTSTATUS
    Controller_WdfEvtDeviceAdd(
        _In_
            WDFDRIVER Driver,
        _Inout_
            PWDFDEVICE_INIT WdfDeviceInit
        )
    {
        NTSTATUS                            status;
        WDFDEVICE                           wdfDevice;
        WDF_PNPPOWER_EVENT_CALLBACKS        wdfPnpPowerCallbacks;
        WDF_OBJECT_ATTRIBUTES               wdfDeviceAttributes;
        WDF_OBJECT_ATTRIBUTES               wdfRequestAttributes;
        UDECX_WDF_DEVICE_CONFIG             controllerConfig;
        WDF_FILEOBJECT_CONFIG               fileConfig;
        PWDFDEVICE_CONTEXT                  pControllerContext;
        WDF_IO_QUEUE_CONFIG                 defaultQueueConfig;
        WDF_DEVICE_POWER_POLICY_IDLE_SETTINGS
                                            idleSettings;
        UNICODE_STRING                      refString;
        ULONG instanceNumber;
        BOOLEAN isCreated;

        DECLARE_UNICODE_STRING_SIZE(uniDeviceName, DeviceNameSize);
        DECLARE_UNICODE_STRING_SIZE(uniSymLinkName, SymLinkNameSize);

        UNREFERENCED_PARAMETER(Driver);

        ...

        WdfDeviceInitSetPnpPowerEventCallbacks(WdfDeviceInit, &wdfPnpPowerCallbacks);

        WDF_OBJECT_ATTRIBUTES_INIT_CONTEXT_TYPE(&wdfRequestAttributes, REQUEST_CONTEXT);
        WdfDeviceInitSetRequestAttributes(WdfDeviceInit, &wdfRequestAttributes);



    // To distinguish I/O sent to GUID_DEVINTERFACE_USB_HOST_CONTROLLER, we will enable
    // enable interface reference strings by calling WdfDeviceInitSetFileObjectConfig
    // with FileObjectClass WdfFileObjectWdfXxx.

    WDF_FILEOBJECT_CONFIG_INIT(&fileConfig,
                                WDF_NO_EVENT_CALLBACK,
                                WDF_NO_EVENT_CALLBACK,
                                WDF_NO_EVENT_CALLBACK // No cleanup callback function
                                );

    ...

    WdfDeviceInitSetFileObjectConfig(WdfDeviceInit,
                                        &fileConfig,
                                        WDF_NO_OBJECT_ATTRIBUTES);

    ...

    // Do additional setup required for USB controllers.

    status = UdecxInitializeWdfDeviceInit(WdfDeviceInit);

    ...

    WDF_OBJECT_ATTRIBUTES_INIT_CONTEXT_TYPE(&wdfDeviceAttributes, WDFDEVICE_CONTEXT);
    wdfDeviceAttributes.EvtCleanupCallback = _ControllerWdfEvtCleanupCallback;


    // Call WdfDeviceCreate with a few extra compatibility steps to ensure this device looks
    // exactly like other USB host controllers.


    isCreated = FALSE;

    for (instanceNumber = 0; instanceNumber < ULONG_MAX; instanceNumber++) {

        status = RtlUnicodeStringPrintf(&uniDeviceName,
                                        L"%ws%d",
                                        BASE_DEVICE_NAME,
                                        instanceNumber);

        ...

        status = WdfDeviceInitAssignName(*WdfDeviceInit, &uniDeviceName);

        ...

        status = WdfDeviceCreate(WdfDeviceInit, WdfDeviceAttributes, WdfDevice);

        if (status == STATUS_OBJECT_NAME_COLLISION) {


            // This is expected to happen at least once when another USB host controller
            // already exists on the system.

        ...

        } else if (!NT_SUCCESS(status)) {

        ...

        } else {

            isCreated = TRUE;
            break;
        }
    }

    if (!isCreated) {

        ...
    }


    // Create the symbolic link (also for compatibility).
    status = RtlUnicodeStringPrintf(&uniSymLinkName,
                                    L"%ws%d",
                                    BASE_SYMBOLIC_LINK_NAME,
                                    instanceNumber);
    ...

    status = WdfDeviceCreateSymbolicLink(*WdfDevice, &uniSymLinkName);

    ...

    // Create the device interface.

    RtlInitUnicodeString(&refString,
                         USB_HOST_DEVINTERFACE_REF_STRING);

    status = WdfDeviceCreateDeviceInterface(wdfDevice,
                                            (LPGUID)&GUID_DEVINTERFACE_USB_HOST_CONTROLLER,
                                            &refString);

    ...

    UDECX_WDF_DEVICE_CONFIG_INIT(&controllerConfig, Controller_EvtUdecxWdfDeviceQueryUsbCapability);

    status = UdecxWdfDeviceAddUsbDeviceEmulation(wdfDevice,
                                               &controllerConfig);


    // Create default queue. It only supports USB controller IOCTLs. (USB I/O will come through
    // in separate USB device queues.)
    // Shown later in this topic.

    WDF_IO_QUEUE_CONFIG_INIT_DEFAULT_QUEUE(&defaultQueueConfig, WdfIoQueueDispatchSequential);
    defaultQueueConfig.EvtIoDeviceControl = ControllerEvtIoDeviceControl;
    defaultQueueConfig.PowerManaged = WdfFalse;

    status = WdfIoQueueCreate(wdfDevice,
                              &defaultQueueConfig,
                              WDF_NO_OBJECT_ATTRIBUTES,
                              &pControllerContext->DefaultQueue);

    ...

    // Initialize virtual USB device software objects.
    // Shown later in this topic.

    status = Usb_Initialize(wdfDevice);

    ...

    exit:

        return status;
    }
    ```


## <a name="handle-user-mode-ioctl-requests-sent-to-the-host-controller"></a>处理发送到主机控制器的用户模式 IOCTL 请求

在初始化期间，UDE 客户端驱动程序将公开 GUID \_ DEVINTERFACE \_ USB \_ 主机 \_ 控制器设备接口 guid。 这样，驱动程序便可从使用该 GUID 打开设备句柄的应用程序接收 IOCTL 请求。 有关 IOCTL 控制代码的列表，请参阅 [Usb IOCTLs for applications and service](/previous-versions/windows/hardware/drivers/ff540046(v=vs.85)#um-ioctl) with 设备 interface GUID： guid \_ DEVINTERFACE \_ USB \_ HOST \_ CONTROLLER。

为了处理这些请求，客户端驱动程序将注册 [*EvtIoDeviceControl*](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_device_control) 事件回调。 在实现中，驱动程序可以选择将请求转发到 UDE 类扩展以便进行处理，而不是处理请求。 若要转发请求，驱动程序必须调用 [**UdecxWdfDeviceTryHandleUserIoctl**](/windows-hardware/drivers/ddi/udecxwdfdevice/nf-udecxwdfdevice-udecxwdfdevicetryhandleuserioctl)。 如果收到的 IOCTL 控制代码对应于标准请求，如检索设备描述符，则类扩展会处理并成功完成请求。 在这种情况下， **UdecxWdfDeviceTryHandleUserIoctl** 将以 TRUE 作为返回值完成。 否则，调用将返回 FALSE，并且驱动程序必须确定如何完成请求。 在最简单的实现中，驱动程序可以通过调用 [**WdfRequestComplete**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcomplete)来完成请求，并提供相应的失败代码。

```cpp

EVT_WDF_IO_QUEUE_IO_DEVICE_CONTROL        Controller_EvtIoDeviceControl;


VOID
Controller_EvtIoDeviceControl(
    _In_
        WDFQUEUE Queue,
    _In_
        WDFREQUEST Request,
    _In_
        size_t OutputBufferLength,
    _In_
        size_t InputBufferLength,
    _In_
        ULONG IoControlCode
)
{
    BOOLEAN handled;
    NTSTATUS status;
    UNREFERENCED_PARAMETER(OutputBufferLength);
    UNREFERENCED_PARAMETER(InputBufferLength);

    handled = UdecxWdfDeviceTryHandleUserIoctl(WdfIoQueueGetDevice(Queue),
                                                Request);

    if (handled) {

        goto exit;
    }

    // Unexpected control code.
    // Fail the request.


    status = STATUS_INVALID_DEVICE_REQUEST;

    WdfRequestComplete(Request, status);

exit:

    return;
}
```

## <a name="report-the-capabilities-of-the-host-controller"></a>报告主机控制器的功能


在上层驱动程序可以使用 USB 主机控制器的功能之前，驱动程序必须确定控制器是否支持这些功能。 驱动程序通过调用 [**WdfUsbTargetDeviceQueryUsbCapability**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicequeryusbcapability) 和 [**USBD \_ QueryUsbCapability**](/previous-versions/windows/hardware/drivers/hh406230(v=vs.85))发出此类查询。 这些调用将转发到 USB 设备仿真 (UDE) 类扩展。 收到请求后，类扩展会调用客户端驱动程序的 [*.Evt \_ UDECX \_ WDF \_ 设备 \_ 查询 \_ USB \_ 功能*](/windows-hardware/drivers/ddi/udecxwdfdevice/nc-udecxwdfdevice-evt_udecx_wdf_device_query_usb_capability) 实现。 此调用仅在 [*EvtDriverDeviceAdd*](/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add) 完成后（通常在 [*EvtDevicePrepareHardware*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware) 中，而不是在 [*EvtDeviceReleaseHardware*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_release_hardware)后）进行。 这是必需的回调函数。

在实现中，客户端驱动程序必须报告它是否支持请求的功能。 UDE （如静态流）不支持某些功能。

```cpp
NTSTATUS
Controller_EvtControllerQueryUsbCapability(
    WDFDEVICE     UdeWdfDevice,
    PGUID         CapabilityType,
    ULONG         OutputBufferLength,
    PVOID         OutputBuffer,
    PULONG        ResultLength
)

{
    NTSTATUS status;

    UNREFERENCED_PARAMETER(UdeWdfDevice);
    UNREFERENCED_PARAMETER(OutputBufferLength);
    UNREFERENCED_PARAMETER(OutputBuffer);

    *ResultLength = 0;

    if (RtlCompareMemory(CapabilityType,
                         &GUID_USB_CAPABILITY_CHAINED_MDLS,
                         sizeof(GUID)) == sizeof(GUID)) {

        //
        // TODO: Is GUID_USB_CAPABILITY_CHAINED_MDLS supported?
        // If supported, status = STATUS_SUCCESS
        // Otherwise, status = STATUS_NOT_SUPPORTED
    }

    else {

        status = STATUS_NOT_IMPLEMENTED;
    }

    return status;
}
```

## <a name="create-a-virtual-usb-device"></a>创建虚拟 USB 设备

虚拟 USB 设备的行为类似于 USB 设备。 它支持具有多个接口的配置，并且每个接口都支持备用设置。 每个设置可以有一个以上的终结点用于数据传输。 所有描述符 (设备、配置、接口、终结点) 由 UDE 客户端驱动程序设置，以便设备能够报告信息，这与真正的 USB 设备非常类似。

> [!NOTE]
> UDE 客户端驱动程序不支持外部集线器

下面是客户端驱动程序为 UDE 设备对象创建 UDECXUSBDEVICE 句柄的序列的摘要。 驱动程序在检索到仿真主机控制器的 WDFDEVICE 句柄之后，必须执行这些步骤。 建议驱动程序在其 [*EvtDriverDeviceAdd*](/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add) 回调函数中执行这些任务。

1. 调用 [**UdecxUsbDeviceInitAllocate**](/windows-hardware/drivers/ddi/udecxusbdevice/nf-udecxusbdevice-udecxusbdeviceinitallocate) 以获取一个指针，该指针指向创建设备所需的初始化参数。 此结构由 UDE 类扩展分配。
2. 通过设置 [**UDECX \_ USB \_ 设备 \_ 状态 \_ 更改 \_ 回调**](/windows-hardware/drivers/ddi/udecxusbdevice/ns-udecxusbdevice-_udecx_usb_device_state_change_callbacks) 的成员，然后调用 [**UdecxUsbDeviceInitSetStateChangeCallbacks**](/windows-hardware/drivers/ddi/udecxusbdevice/nf-udecxusbdevice-udecxusbdeviceinitsetstatechangecallbacks)来注册事件回调函数。 下面是与 UDE 设备对象相关联的回调函数，由 UDE 类扩展调用。

    这些函数由客户端驱动程序实现，以创建或配置终结点。

   - [*.EVT \_ UDECX \_ USB \_ 设备 \_ 默认 \_ 终结点 \_ 添加*](/windows-hardware/drivers/ddi/udecxusbdevice/nc-udecxusbdevice-evt_udecx_usb_device_default_endpoint_add)
   - [*.EVT \_ UDECX \_ USB \_ 设备 \_ 终结点 \_ 添加*](/windows-hardware/drivers/ddi/udecxusbdevice/nc-udecxusbdevice-evt_udecx_usb_device_endpoint_add)
   - [*.EVT \_ UDECX \_ USB \_ 设备 \_ 终结点 \_ 配置*](/windows-hardware/drivers/ddi/udecxusbdevice/nc-udecxusbdevice-evt_udecx_usb_device_endpoints_configure)

     <!-- -->

   - [*.EVT \_ UDECX \_ USB \_ 设备 \_ D0 \_ 条目*](/windows-hardware/drivers/ddi/udecxusbdevice/nc-udecxusbdevice-evt_udecx_usb_device_d0_entry)
   - [*.EVT \_ UDECX \_ USB \_ 设备 \_ D0 \_ 出口*](/windows-hardware/drivers/ddi/udecxusbdevice/nc-udecxusbdevice-evt_udecx_usb_device_d0_exit)
   - [*.EVT \_ UDECX \_ USB \_ 设备 \_ 集 \_ 函数 \_ 挂起 \_ 和 \_ 唤醒*](/windows-hardware/drivers/ddi/udecxusbdevice/nc-udecxusbdevice-evt_udecx_usb_device_set_function_suspend_and_wake)

3. 调用 [**UdecxUsbDeviceInitSetSpeed**](/windows-hardware/drivers/ddi/udecxusbdevice/nf-udecxusbdevice-udecxusbdeviceinitsetspeed) 设置 usb 设备速度以及设备类型、usb 2.0 或 SuperSpeed 设备。
4. 调用 [**UdecxUsbDeviceInitSetEndpointsType**](/windows-hardware/drivers/ddi/udecxusbdevice/nf-udecxusbdevice-udecxusbdeviceinitsetendpointstype) 可指定设备支持的终结点类型：简单或动态。 如果客户端驱动程序选择创建简单的终结点，则驱动程序必须在插入设备之前创建所有终结点对象。 设备只能有一个配置，并且每个接口只需要一个接口设置。 对于动态终结点，驱动程序可以在设备接收到 [*.Evt \_ UDECX \_ USB \_ 设备 \_ 终结点 \_ *](/windows-hardware/drivers/ddi/udecxusbdevice/nc-udecxusbdevice-evt_udecx_usb_device_endpoints_configure) 时随时创建终结点。 请参阅 [创建动态终结点](#create-dynamic-endpoints)。
5. 调用这些方法中的任何一种，将所需的描述符添加到设备。

   - [**UdecxUsbDeviceInitAddDescriptor**](/windows-hardware/drivers/ddi/udecxusbdevice/nf-udecxusbdevice-udecxusbdeviceinitadddescriptor)
   - [**UdecxUsbDeviceInitAddDescriptorWithIndex**](/windows-hardware/drivers/ddi/udecxusbdevice/nf-udecxusbdevice-udecxusbdeviceinitadddescriptorwithindex)
   - [**UdecxUsbDeviceInitAddStringDescriptor**](/windows-hardware/drivers/ddi/udecxusbdevice/nf-udecxusbdevice-udecxusbdeviceinitaddstringdescriptor)
   - [**UdecxUsbDeviceInitAddStringDescriptorRaw**](/windows-hardware/drivers/ddi/udecxusbdevice/nf-udecxusbdevice-udecxusbdeviceinitaddstringdescriptorraw)

     如果 UDE 类扩展接收到客户端驱动程序在初始化期间通过使用上述方法之一提供的标准描述符的请求，则类扩展会自动完成该请求。 类扩展不会将该请求转发到客户端驱动程序。 此设计减少了驱动程序处理控制请求所需的请求数。 此外，它还无需驱动程序实现描述符逻辑，需要对安装包进行大量分析并正确处理 **wLength** 和 **TransferBufferLength** 。 此列表包含标准请求。 仅当调用前面的方法来添加描述符) ，客户端驱动程序才需要检查这些请求 (：

   - USB \_ 请求 \_ 获取 \_ 描述符
   - USB \_ 请求 \_ 设置 \_ 配置
   - USB \_ 请求 \_ 集 \_ 接口
   - USB \_ 请求 \_ 集 \_ 地址
   - USB \_ 请求 \_ 集 \_ 功能
   - USB \_ 功能 \_ 函数 \_ 挂起
   - USB \_ 功能 \_ 远程 \_ 唤醒
   - USB \_ 请求 \_ 清除 \_ 功能
   - USB \_ 功能 \_ 终结点 \_ 停止
   - USB \_ 请求 \_ 集 \_ SEL
   - USB \_ 请求 \_ ISOCH \_ 延迟

     但是，对于接口、类特定或供应商定义的描述符的请求，UDE 类扩展会将它们转发到客户端驱动程序。 驱动程序必须处理这些 GET \_ 说明符请求。

6. 调用 [**UdecxUsbDeviceCreate**](/windows-hardware/drivers/ddi/udecxusbdevice/nf-udecxusbdevice-udecxusbdevicecreate) 创建 UDE 设备对象并检索 UDECXUSBDEVICE 句柄。
7. 通过调用 [**UdecxUsbEndpointCreate**](/windows-hardware/drivers/ddi/udecxusbendpoint/nf-udecxusbendpoint-udecxusbendpointcreate)创建静态终结点。 请参阅 [创建简单终结点](#create-simple-endpoints)。
8. 调用 [**UdecxUsbDevicePlugIn**](/windows-hardware/drivers/ddi/udecxusbdevice/nf-udecxusbdevice-udecxusbdeviceplugin) ，向 UDE 类扩展指示设备已连接，并可在终结点上接收 i/o 请求。 在此调用之后，类扩展还可以对终结点和 USB 设备调用回调函数。
    **注意**  如果 USB 设备需要在运行时删除，则客户端驱动程序可以调用 [**UdecxUsbDevicePlugOutAndDelete**](/windows-hardware/drivers/ddi/udecxusbdevice/nf-udecxusbdevice-udecxusbdeviceplugoutanddelete)。 如果驱动程序要使用该设备，则必须通过调用 [**UdecxUsbDeviceCreate**](/windows-hardware/drivers/ddi/udecxusbdevice/nf-udecxusbdevice-udecxusbdevicecreate)来创建它。

在此示例中，说明符声明被假定为全局变量，如此处所示，作为示例：

```cpp
const UCHAR g_UsbDeviceDescriptor[] = {
    // Device Descriptor
    0x12, // Descriptor Size
    0x01, // Device Descriptor Type
    0x00, 0x03, // USB 3.0
    0x00, // Device class
    0x00, // Device sub-class
    0x00, // Device protocol
    0x09, // Maxpacket size for EP0 : 2^9
    0x5E, 0x04, // Vendor ID
    0x39, 0x00, // Product ID
    0x00, // LSB of firmware version
    0x03, // MSB of firmware version
    0x01, // Manufacture string index
    0x03, // Product string index
    0x00, // Serial number string index
    0x01 // Number of configurations
};
```

下面是一个示例，其中，客户端驱动程序通过注册回调函数来指定初始化参数，设置设备速度，指示终结点的类型，最后设置某些设备描述符。

```cpp

NTSTATUS
Usb_Initialize(
    _In_
        WDFDEVICE WdfDevice
    )
{
    NTSTATUS                                status;
    PUSB_CONTEXT                            usbContext;    //Client driver declared context for the host controller object
    PUDECX_USBDEVICE_CONTEXT                deviceContext; //Client driver declared context for the UDE device object
    UDECX_USB_DEVICE_STATE_CHANGE_CALLBACKS callbacks;
    WDF_OBJECT_ATTRIBUTES                   attributes;

    UDECX_USB_DEVICE_PLUG_IN_OPTIONS        pluginOptions;


    usbContext = WdfDeviceGetUsbContext(WdfDevice);

    usbContext->UdecxUsbDeviceInit = UdecxUsbDeviceInitAllocate(WdfDevice);

    if (usbContext->UdecxUsbDeviceInit == NULL) {

        ...
        goto exit;
    }


    // State changed callbacks

    UDECX_USB_DEVICE_CALLBACKS_INIT(&callbacks);
#ifndef SIMPLEENDPOINTS
    callbacks.EvtUsbDeviceDefaultEndpointAdd = UsbDevice_EvtUsbDeviceDefaultEndpointAdd;
    callbacks.EvtUsbDeviceEndpointAdd = UsbDevice_EvtUsbDeviceEndpointAdd;
    callbacks.EvtUsbDeviceEndpointsConfigure = UsbDevice_EvtUsbDeviceEndpointsConfigure;
#endif
    callbacks.EvtUsbDeviceLinkPowerEntry = UsbDevice_EvtUsbDeviceLinkPowerEntry;
    callbacks.EvtUsbDeviceLinkPowerExit = UsbDevice_EvtUsbDeviceLinkPowerExit;
    callbacks.EvtUsbDeviceSetFunctionSuspendAndWake = UsbDevice_EvtUsbDeviceSetFunctionSuspendAndWake;

    UdecxUsbDeviceInitSetStateChangeCallbacks(usbContext->UdecxUsbDeviceInit, &callbacks);


    // Set required attributes.

    UdecxUsbDeviceInitSetSpeed(usbContext->UdecxUsbDeviceInit, UdecxUsbLowSpeed);

#ifdef SIMPLEENDPOINTS
    UdecxUsbDeviceInitSetEndpointsType(usbContext->UdecxUsbDeviceInit, UdecxEndpointTypeSimple);
#else
    UdecxUsbDeviceInitSetEndpointsType(usbContext->UdecxUsbDeviceInit, UdecxEndpointTypeDynamic);
#endif


    // Add device descriptor
    //
    status = UdecxUsbDeviceInitAddDescriptor(usbContext->UdecxUsbDeviceInit,
                                           (PUCHAR)g_UsbDeviceDescriptor,
                                           sizeof(g_UsbDeviceDescriptor));

    if (!NT_SUCCESS(status)) {

        goto exit;
    }

#ifdef USB30

    // Add BOS descriptor for a SuperSpeed device

    status = UdecxUsbDeviceInitAddDescriptor(pUsbContext->UdecxUsbDeviceInit,
                                           (PUCHAR)g_UsbBOSDescriptor,
                                           sizeof(g_UsbBOSDescriptor));

    if (!NT_SUCCESS(status)) {

        goto exit;
    }
#endif


    // String descriptors

    status = UdecxUsbDeviceInitAddDescriptorWithIndex(usbContext->UdecxUsbDeviceInit,
                                                    (PUCHAR)g_LanguageDescriptor,
                                                    sizeof(g_LanguageDescriptor),
                                                    0);

    if (!NT_SUCCESS(status)) {

        goto exit;
    }

    status = UdecxUsbDeviceInitAddStringDescriptor(usbContext->UdecxUsbDeviceInit,
                                                 &g_ManufacturerStringEnUs,
                                                 g_ManufacturerIndex,
                                                 US_ENGLISH);

    if (!NT_SUCCESS(status)) {

        goto exit;
    }

    WDF_OBJECT_ATTRIBUTES_INIT_CONTEXT_TYPE(&attributes, UDECX_USBDEVICE_CONTEXT);

    status = UdecxUsbDeviceCreate(&usbContext->UdecxUsbDeviceInit,
                                &attributes,
                                &usbContext->UdecxUsbDevice);

    if (!NT_SUCCESS(status)) {

        goto exit;
    }

#ifdef SIMPLEENDPOINTS
   // Create the default control endpoint
   // Shown later in this topic.

    status = UsbCreateControlEndpoint(WdfDevice);

    if (!NT_SUCCESS(status)) {

        goto exit;
    }

#endif

    UDECX_USB_DEVICE_PLUG_IN_OPTIONS_INIT(&pluginOptions);
#ifdef USB30
    pluginOptions.Usb30PortNumber = 2;
#else
    pluginOptions.Usb20PortNumber = 1;
#endif
    status = UdecxUsbDevicePlugIn(usbContext->UdecxUsbDevice, &pluginOptions);

exit:

    if (!NT_SUCCESS(status)) {

        UdecxUsbDeviceInitFree(usbContext->UdecxUsbDeviceInit);
        usbContext->UdecxUsbDeviceInit = NULL;

    }

    return status;
}
```

## <a name="power-management-of-the-usb-device"></a>USB 设备的电源管理


当 UDE 类扩展接收到将设备发送到低功耗状态或使其恢复正常工作状态的请求时，将调用客户端驱动程序的回调函数。 支持唤醒的 USB 设备需要这些回调函数。 客户端驱动程序在先前对 [**UdecxUsbDeviceInitSetStateChangeCallbacks**](/windows-hardware/drivers/ddi/udecxusbdevice/nf-udecxusbdevice-udecxusbdeviceinitsetstatechangecallbacks)的调用中注册了其实现。

有关详细信息，请参阅 [USB 设备电源状态](comparing-usb-device-states-to-wdm-device-states.md)。

[*.EVT \_ UDECX \_ USB \_ 设备 \_ D0 \_ 条目*](/windows-hardware/drivers/ddi/udecxusbdevice/nc-udecxusbdevice-evt_udecx_usb_device_d0_entry)  
客户端驱动程序将设备从 Dx 状态转换为 D0 状态。

[*.EVT \_ UDECX \_ USB \_ 设备 \_ D0 \_ 出口*](/windows-hardware/drivers/ddi/udecxusbdevice/nc-udecxusbdevice-evt_udecx_usb_device_d0_exit)  
客户端驱动程序将设备从 D0 状态转换为 Dx 状态。

[*.EVT \_ UDECX \_ USB \_ 设备 \_ 集 \_ 函数 \_ 挂起 \_ 和 \_ 唤醒*](/windows-hardware/drivers/ddi/udecxusbdevice/nc-udecxusbdevice-evt_udecx_usb_device_set_function_suspend_and_wake)  
客户端驱动程序更改虚拟 USB 3.0 设备的指定接口的函数状态。

USB 3.0 设备允许各个功能进入较低的电源状态。 每个函数还能够发送唤醒信号。 UDE 类扩展通过调用 [*.Evt \_ UDECX \_ USB \_ 设备 \_ 集 \_ 函数 \_ 挂起 \_ 和 \_ 唤醒*](/windows-hardware/drivers/ddi/udecxusbdevice/nc-udecxusbdevice-evt_udecx_usb_device_set_function_suspend_and_wake)通知客户端驱动程序。 此事件表示函数电源状态更改，并向客户端驱动程序通知该函数是否可以从新状态中唤醒。 在函数中，类扩展传递正在唤醒的函数的接口号。
客户端驱动程序可以模拟虚拟 USB 设备的操作，该设备从低链路电源状态和/或函数挂起启动自己的唤醒。 对于 USB 2.0 设备，如果驱动程序已在最新的[*.Evt \_ UDECX \_ USB \_ 设备 \_ D0 \_ 出口*](/windows-hardware/drivers/ddi/udecxusbdevice/nc-udecxusbdevice-evt_udecx_usb_device_d0_exit)启用设备唤醒，则驱动程序必须调用[**UdecxUsbDeviceSignalWake**](/windows-hardware/drivers/ddi/udecxusbdevice/nf-udecxusbdevice-udecxusbdevicesignalwake)。 对于 USB 3.0 设备，驱动程序必须调用 [**UdecxUsbDeviceSignalFunctionWake**](/windows-hardware/drivers/ddi/udecxusbdevice/nf-udecxusbdevice-udecxusbdevicesignalfunctionwake) ，因为 USB 3.0 唤醒功能是每个函数的。 如果整个设备处于低功耗状态，或进入此类状态， **UdecxUsbDeviceSignalFunctionWake** 将唤醒设备。

## <a name="create-simple-endpoints"></a>创建简单终结点


客户端驱动程序创建 UDE 终结点对象来处理传入和传出 USB 设备的数据传输。 驱动程序在创建 UDE 设备后以及将设备报告为接通电源之前，会创建简单的终结点。

下面是客户端驱动程序为 UDE 终结点对象创建 UDECXUSBENDPOINT 句柄的序列的摘要。 驱动程序在检索虚拟 USB 设备的 UDECXUSBDEVICE 句柄之后必须执行这些步骤。 建议驱动程序在其 [*EvtDriverDeviceAdd*](/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add) 回调函数中执行这些任务。

1. 调用 [**UdecxUsbSimpleEndpointInitAllocate**](/windows-hardware/drivers/ddi/udecxusbendpoint/nf-udecxusbendpoint-udecxusbsimpleendpointinitallocate) 以获取指向类扩展所分配的初始化参数的指针。
2. 调用 [**UdecxUsbEndpointInitSetEndpointAddress**](/windows-hardware/drivers/ddi/udecxusbendpoint/nf-udecxusbendpoint-udecxusbendpointinitsetendpointaddress) ，以在初始化参数中设置终结点地址。
3. 调用 [**UdecxUsbEndpointInitSetCallbacks**](/windows-hardware/drivers/ddi/udecxusbendpoint/nf-udecxusbendpoint-udecxusbendpointinitsetcallbacks) 以注册客户端驱动程序实现的回调函数。

    这些函数由客户端驱动程序实现以处理对终结点的队列和请求。

    [*.EVT \_ UDECX \_ USB \_ 终结点 \_ 重置*](/windows-hardware/drivers/ddi/udecxusbendpoint/nc-udecxusbendpoint-evt_udecx_usb_endpoint_reset)  
    重置虚拟 USB 设备的终结点。

    [*.EVT \_ UDECX \_ USB \_ 终结点 \_ 启动*](/windows-hardware/drivers/ddi/udecxusbendpoint/nc-udecxusbendpoint-evt_udecx_usb_endpoint_start)  
    可选。 开始处理 i/o 请求

    [*.EVT \_ UDECX \_ USB \_ 终结点 \_ 清除*](/windows-hardware/drivers/ddi/udecxusbendpoint/nc-udecxusbendpoint-evt_udecx_usb_endpoint_purge)  
    可选。 停止对终结点队列的 i/o 请求进行排队并取消未处理的请求。

4. 调用 [**UdecxUsbEndpointCreate**](/windows-hardware/drivers/ddi/udecxusbendpoint/nf-udecxusbendpoint-udecxusbendpointcreate) 创建终结点对象并检索 UDECXUSBENDPOINT 句柄。
5. 调用 [**UdecxUsbEndpointSetWdfIoQueue**](/windows-hardware/drivers/ddi/udecxusbendpoint/nf-udecxusbendpoint-udecxusbendpointsetwdfioqueue) ，将框架队列对象与终结点相关联。 如果适用，则可以通过设置适当的属性，将终结点对象设置为队列的 WDF 父对象。

    每个终结点对象都有一个框架队列对象，以便处理传输请求。 对于类扩展接收的每个传输请求，它会将框架请求对象排队。 队列状态 (已启动，已清除) 由 UDE 类扩展管理，客户端驱动程序不得更改该状态。 每个请求对象都包含一个 USB 请求块 (包含传输详细信息的 [**URB**](/windows-hardware/drivers/ddi/usb/ns-usb-_urb)) 。

在此示例中，客户端驱动程序将创建默认的控制终结点。

```cpp
EVT_WDF_IO_QUEUE_IO_INTERNAL_DEVICE_CONTROL IoEvtControlUrb;
EVT_UDECX_USB_ENDPOINT_RESET UsbEndpointReset;
EVT_UDECX_USB_ENDPOINT_PURGE UsEndpointEvtPurge;
EVT_UDECX_USB_ENDPOINT_START UsbEndpointEvtStart;

NTSTATUS
UsbCreateControlEndpoint(
    _In_
        WDFDEVICE WdfDevice
    )
{
    NTSTATUS                      status;
    PUSB_CONTEXT                  pUsbContext;
    WDF_IO_QUEUE_CONFIG           queueConfig;
    WDFQUEUE                      controlQueue;
    UDECX_USB_ENDPOINT_CALLBACKS  callbacks;
    PUDECXUSBENDPOINT_INIT        endpointInit;

    pUsbContext = WdfDeviceGetUsbContext(WdfDevice);
    endpointInit = NULL;

    WDF_IO_QUEUE_CONFIG_INIT(&queueConfig, WdfIoQueueDispatchSequential);

    queueConfig.EvtIoInternalDeviceControl = IoEvtControlUrb;

    status = WdfIoQueueCreate (Device,
                               &queueConfig,
                               WDF_NO_OBJECT_ATTRIBUTES,
                               &controlQueue);


    if (!NT_SUCCESS(status)) {

        goto exit;
    }

    endpointInit = UdecxUsbSimpleEndpointInitAllocate(pUsbContext->UdecxUsbDevice);

    if (endpointInit == NULL) {

        status = STATUS_INSUFFICIENT_RESOURCES;
        goto exit;
    }

    UdecxUsbEndpointInitSetEndpointAddress(endpointInit, USB_DEFAULT_ENDPOINT_ADDRESS);

    UDECX_USB_ENDPOINT_CALLBACKS_INIT(&callbacks, UsbEndpointReset);
    UdecxUsbEndpointInitSetCallbacks(endpointInit, &callbacks);

    callbacks.EvtUsbEndpointStart = UsbEndpointEvtStart;
    callbacks.EvtUsbEndpointPurge = UsEndpointEvtPurge;

    status = UdecxUsbEndpointCreate(&endpointInit,
        WDF_NO_OBJECT_ATTRIBUTES,
        &pUsbContext->UdecxUsbControlEndpoint);

    if (!NT_SUCCESS(status)) {
        goto exit;
    }

    UdecxUsbEndpointSetWdfIoQueue(pUsbContext->UdecxUsbControlEndpoint,
        controlQueue);

exit:

    if (endpointInit != NULL) {

        NT_ASSERT(!NT_SUCCESS(status));
        UdecxUsbEndpointInitFree(endpointInit);
        endpointInit = NULL;
    }

    return status;
}
```

## <a name="create-dynamic-endpoints"></a>创建动态终结点


客户端驱动程序可 (代表集线器驱动程序和客户端驱动程序) 在请求 UDE 类扩展时创建动态终结点。 类扩展通过调用以下任一回调函数发出请求：

[*.EVT \_ UDECX \_ USB \_ 设备 \_ 默认 \_ 终结点 \_ 添加*](/windows-hardware/drivers/ddi/udecxusbdevice/nc-udecxusbdevice-evt_udecx_usb_device_default_endpoint_add)  
客户端驱动程序将创建默认的控制终结点 (端点 0) 

[*.EVT \_ UDECX \_ USB \_ 设备 \_ 终结点 \_ 添加*](/windows-hardware/drivers/ddi/udecxusbdevice/nc-udecxusbdevice-evt_udecx_usb_device_endpoint_add)  
客户端驱动程序创建动态端点。

[*.EVT \_ UDECX \_ USB \_ 设备 \_ 终结点 \_ 配置*](/windows-hardware/drivers/ddi/udecxusbdevice/nc-udecxusbdevice-evt_udecx_usb_device_endpoints_configure)  
客户端驱动程序通过选择替代设置、禁用当前终结点或添加动态终结点来更改配置。

客户端驱动程序在其对 [**UdecxUsbDeviceInitSetStateChangeCallbacks**](/windows-hardware/drivers/ddi/udecxusbdevice/nf-udecxusbdevice-udecxusbdeviceinitsetstatechangecallbacks)的调用过程中注册了前面的回调。 请参阅创建 [虚拟 USB 设备](#create-a-virtual-usb-device)。
此机制允许客户端驱动程序在设备上动态更改 USB 配置和接口设置。 例如，需要终结点对象或必须释放现有终结点对象时，类扩展将调用 [* \_ UDECX \_ USB \_ 设备 \_ 终结点 \_ *](/windows-hardware/drivers/ddi/udecxusbdevice/nc-udecxusbdevice-evt_udecx_usb_device_endpoints_configure)。

下面是客户端驱动程序在其回调函数实现中为终结点对象创建 UDECXUSBENDPOINT 句柄的序列的摘要。

1. 调用 [**UdecxUsbEndpointInitSetEndpointAddress**](/windows-hardware/drivers/ddi/udecxusbendpoint/nf-udecxusbendpoint-udecxusbendpointinitsetendpointaddress) ，以在初始化参数中设置终结点地址。
2. 调用 [**UdecxUsbEndpointInitSetCallbacks**](/windows-hardware/drivers/ddi/udecxusbendpoint/nf-udecxusbendpoint-udecxusbendpointinitsetcallbacks) 以注册客户端驱动程序实现的回调函数。 与简单终结点类似，驱动程序可以注册以下回调函数：
    - [*.Evt \_UDECX \_ USB \_ 终结点 \_ 重置*](/windows-hardware/drivers/ddi/udecxusbendpoint/nc-udecxusbendpoint-evt_udecx_usb_endpoint_reset) (需要) 。
    - [*.EVT \_ UDECX \_ USB \_ 终结点 \_ 启动*](/windows-hardware/drivers/ddi/udecxusbendpoint/nc-udecxusbendpoint-evt_udecx_usb_endpoint_start)
    - [*.EVT \_ UDECX \_ USB \_ 终结点 \_ 清除*](/windows-hardware/drivers/ddi/udecxusbendpoint/nc-udecxusbendpoint-evt_udecx_usb_endpoint_purge)

3. 调用 [**UdecxUsbEndpointCreate**](/windows-hardware/drivers/ddi/udecxusbendpoint/nf-udecxusbendpoint-udecxusbendpointcreate) 创建终结点对象并检索 UDECXUSBENDPOINT 句柄。
4. 调用 [**UdecxUsbEndpointSetWdfIoQueue**](/windows-hardware/drivers/ddi/udecxusbendpoint/nf-udecxusbendpoint-udecxusbendpointsetwdfioqueue) ，将框架队列对象与终结点相关联。

在此示例实现中，客户端驱动程序创建动态的默认控制终结点。

```cpp
NTSTATUS
UsbDevice_EvtUsbDeviceDefaultEndpointAdd(
    _In_
        UDECXUSBDEVICE            UdecxUsbDevice,
    _In_
        PUDECXUSBENDPOINT_INIT    UdecxUsbEndpointInit
)
{
    NTSTATUS                    status;
    PUDECX_USBDEVICE_CONTEXT    deviceContext;
    WDFQUEUE                    controlQueue;
    WDF_IO_QUEUE_CONFIG         queueConfig;
    UDECX_USB_ENDPOINT_CALLBACKS  callbacks;

    deviceContext = UdecxDeviceGetContext(UdecxUsbDevice);

    WDF_IO_QUEUE_CONFIG_INIT(&queueConfig, WdfIoQueueDispatchSequential);

    queueConfig.EvtIoInternalDeviceControl = IoEvtControlUrb;

    status = WdfIoQueueCreate (deviceContext->WdfDevice,
                               &queueConfig,
                               WDF_NO_OBJECT_ATTRIBUTES,
                               &controlQueue);

    if (!NT_SUCCESS(status)) {

        goto exit;
    }

    UdecxUsbEndpointInitSetEndpointAddress(UdecxUsbEndpointInit, USB_DEFAULT_DEVICE_ADDRESS);

    UDECX_USB_ENDPOINT_CALLBACKS_INIT(&callbacks, UsbEndpointReset);
    UdecxUsbEndpointInitSetCallbacks(UdecxUsbEndpointInit, &callbacks);

    status = UdecxUsbEndpointCreate(UdecxUsbEndpointInit,
        WDF_NO_OBJECT_ATTRIBUTES,
        &deviceContext->UdecxUsbControlEndpoint);

    if (!NT_SUCCESS(status)) {
        goto exit;
    }

    UdecxUsbEndpointSetWdfIoQueue(deviceContext->UdecxUsbControlEndpoint,
        controlQueue);


exit:

    return status;
}
```

## <a name="perform-error-recovery-by-resetting-an-endpoint"></a>通过重置终结点来执行错误恢复


有时，数据传输会因各种原因而失败，例如终结点中的延迟情况。 如果传输失败，则直到清除错误条件后，终结点才能处理请求。 当 UDE 类扩展遇到失败的数据传输时，它将调用客户端驱动程序的 [*.Evt \_ UDECX \_ USB \_ 终结点 \_ 重置*](/windows-hardware/drivers/ddi/udecxusbendpoint/nc-udecxusbendpoint-evt_udecx_usb_endpoint_reset) 回调函数，该函数将在之前对 [**UdecxUsbEndpointInitSetCallbacks**](/windows-hardware/drivers/ddi/udecxusbendpoint/nf-udecxusbendpoint-udecxusbendpointinitsetcallbacks)的调用中注册该函数。 在实现中，驱动程序可以选择清除管道的暂停状态，并采取其他必要的步骤来清除错误情况。

此调用是异步的。 使用重置操作完成客户端之后，驱动程序必须通过调用 [**WdfRequestComplete**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcomplete)来完成请求，并提供相应的失败代码。 该调用会向 UDE 客户端扩展通知完成重置操作的状态。

**注意**  如果错误恢复需要复杂的解决方案，则客户端驱动程序可以选择重置主机控制器。 此逻辑可在该驱动程序在其[**UdecxWdfDeviceAddUsbDeviceEmulation**](/windows-hardware/drivers/ddi/udecxwdfdevice/nf-udecxwdfdevice-udecxwdfdeviceaddusbdeviceemulation)调用中注册的[*.Evt \_ UDECX \_ WDF \_ 设备 \_ RESET*](/windows-hardware/drivers/ddi/udecxwdfdevice/nc-udecxwdfdevice-evt_udecx_wdf_device_reset)回调函数中实现。 如果适用，驱动程序可以重置主机控制器和所有下游设备。 如果客户端驱动程序不需要重置控制器但重置所有下游设备，则驱动程序必须在注册过程中在配置参数中指定 **UdeWdfDeviceResetActionResetEachUsbDevice** 。 在这种情况下，类扩展会为每个连接的设备调用 *.Evt \_ UDECX \_ WDF \_ 设备 \_ 重置* 。

## <a name="implement-queue-state-management"></a>实现队列状态管理

与 UDE 终结点对象关联的框架队列对象的状态由 UDE 类扩展管理。 但是，如果客户端驱动程序将来自终结点队列的请求转发到其他内部队列，则客户端必须实现逻辑来处理终结点的 i/o 流中的更改。 这些回调函数已注册到 [**UdecxUsbEndpointInitSetCallbacks**](/windows-hardware/drivers/ddi/udecxusbendpoint/nf-udecxusbendpoint-udecxusbendpointinitsetcallbacks)。

### <a name="endpoint-purge-operation"></a>终结点清除操作

每个终结点有一个队列的 UDE 客户端驱动程序可以实现 [*.Evt \_ UDECX \_ USB \_ 终结点 \_ 清除*](/windows-hardware/drivers/ddi/udecxusbendpoint/nc-udecxusbendpoint-evt_udecx_usb_endpoint_purge) ，如以下示例中所示：

在 [*.Evt \_ UDECX \_ USB \_ 终结点 \_ 清除*](/windows-hardware/drivers/ddi/udecxusbendpoint/nc-udecxusbendpoint-evt_udecx_usb_endpoint_purge) 实现中，需要客户端驱动程序，以确保已完成从终结点队列转发的所有 i/o，并且在调用客户端驱动程序的 [*.evt \_ UDECX \_ USB \_ 终结点 \_ 启动*](/windows-hardware/drivers/ddi/udecxusbendpoint/nc-udecxusbendpoint-evt_udecx_usb_endpoint_start) 之前，新转发的 i/o 也会失败。 这些要求是通过调用 [**UdecxUsbEndpointPurgeComplete**](/windows-hardware/drivers/ddi/udecxusbendpoint/nf-udecxusbendpoint-udecxusbendpointpurgecomplete)来实现的，这可确保所有已转发的 i/o 已完成，且将来的已转发 i/o 失败。

### <a name="endpoint-start-operation"></a>终结点启动操作

在 [*.Evt \_ UDECX \_ USB \_ 终结点 \_ 启动*](/windows-hardware/drivers/ddi/udecxusbendpoint/nc-udecxusbendpoint-evt_udecx_usb_endpoint_start) 实现中，需要客户端驱动程序来开始处理终结点队列上的 i/o 以及接收终结点的已转发 i/o 的任何队列。 创建终结点后，在此回调函数返回后，它不会接收任何 i/o。 此回调将终结点返回到在 [* \_ UDECX \_ USB \_ 终结点 \_ 清除*](/windows-hardware/drivers/ddi/udecxusbendpoint/nc-udecxusbendpoint-evt_udecx_usb_endpoint_purge) 完成后处理 i/o 状态。


## <a name="handling-data-transfer-requests-urbs"></a>处理数据传输请求 (URBs) 


若要处理发送到客户端设备终结点的 USB i/o 请求，请在将队列与终结点关联时，截获与[**UdecxUsbEndpointInitSetCallbacks**](/windows-hardware/drivers/ddi/udecxusbendpoint/nf-udecxusbendpoint-udecxusbendpointinitsetcallbacks)一起使用的队列对象上的[EVT_WDF_IO_QUEUE_IO_INTERNAL_DEVICE_CONTROL](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_internal_device_control)回调。 在此回调中，对 [IOCTL \_ 内部 \_ USB \_ SUBMIT \_ URB](/windows-hardware/drivers/ddi/usbioctl/ni-usbioctl-ioctl_internal_usb_submit_urb) IoControlCode 的 i/o 进行处理 (参阅 [URB 处理方法](#urb-handling-methods)) 下的示例代码。


## <a name="urb-handling-methods"></a>URB 处理方法


作为通过 [IOCTL \_ 内部 \_ USB \_ 提交 \_ URB](/windows-hardware/drivers/ddi/usbioctl/ni-usbioctl-ioctl_internal_usb_submit_urb) 的 URBs 的一部分，与虚拟设备上的终结点相关联的队列，UDE 客户端驱动程序可以使用以下方法获取指向 i/o 请求传输缓冲区的指针：

这些函数由客户端驱动程序实现以处理对终结点的队列和请求。

[**UdecxUrbRetrieveControlSetupPacket**](/windows-hardware/drivers/ddi/udecxurb/nf-udecxurb-udecxurbretrievecontrolsetuppacket)  
检索指定框架请求对象中的 USB 控件安装包。

[**UdecxUrbRetrieveBuffer**](/windows-hardware/drivers/ddi/udecxurb/nf-udecxurb-udecxurbretrievebuffer)  
从发送到终结点队列的指定框架请求对象检索 URB 的传输缓冲区。

[**UdecxUrbSetBytesCompleted**](/windows-hardware/drivers/ddi/udecxurb/nf-udecxurb-udecxurbsetbytescompleted)  
设置框架请求对象中包含的 URB 传输的字节数。

[**UdecxUrbComplete**](/windows-hardware/drivers/ddi/udecxurb/nf-udecxurb-udecxurbcomplete)  
完成具有 USB 特定完成状态代码的 URB 请求。

[**UdecxUrbCompleteWithNtStatus**](/windows-hardware/drivers/ddi/udecxurb/nf-udecxurb-udecxurbcompletewithntstatus)  
使用 NTSTATUS 代码完成 URB 请求。

下面是 URB USB 传出传输的典型 i/o 处理流程。

```cpp
static VOID
IoEvtSampleOutUrb(
    _In_ WDFQUEUE Queue,
    _In_ WDFREQUEST Request,
    _In_ size_t OutputBufferLength,
    _In_ size_t InputBufferLength,
    _In_ ULONG IoControlCode
)
{
    PENDPOINTQUEUE_CONTEXT pEpQContext;
    NTSTATUS status = STATUS_SUCCESS;
    PUCHAR transferBuffer;
    ULONG transferBufferLength = 0;

    UNREFERENCED_PARAMETER(OutputBufferLength);
    UNREFERENCED_PARAMETER(InputBufferLength);

    // one possible way to get context info
    pEpQContext = GetEndpointQueueContext(Queue);

    if (IoControlCode != IOCTL_INTERNAL_USB_SUBMIT_URB)
    {
        LogError(TRACE_DEVICE, "WdfRequest %p Incorrect IOCTL %x, %!STATUS!",
            Request, IoControlCode, status);
        status = STATUS_INVALID_PARAMETER;
        goto exit;
    }

    status = UdecxUrbRetrieveBuffer(Request, &transferBuffer, &transferBufferLength);
    if (!NT_SUCCESS(status))
    {
        LogError(TRACE_DEVICE, "WdfRequest %p unable to retrieve buffer %!STATUS!",
            Request, status);
        goto exit;
    }

    if (transferBufferLength >= 1)
    {
        //consume one byte of output data
        pEpQContext->global_storage = transferBuffer[0];
    }

exit:
    // writes never pended, always completed
    UdecxUrbSetBytesCompleted(Request, transferBufferLength);
    UdecxUrbCompleteWithNtStatus(Request, status);
    return;
}
```

客户端驱动程序可以在单独的 DPC 上完成 i/o 请求。 遵循以下最佳实践：

- 若要确保与现有 USB 驱动程序兼容，UDE 客户端必须在派单级别调用 [**WdfRequestComplete**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcomplete) \_ 。
- 如果 [**URB**](/windows-hardware/drivers/ddi/usb/ns-usb-_urb) 已添加到终结点的队列中，并且驱动程序开始在调用驱动程序的线程或 DPC 上同步处理它，则请求不得同步完成。 此用途需要单独的 DPC，驱动程序将通过调用 [**WdfDpcEnqueue**](/windows-hardware/drivers/ddi/wdfdpc/nf-wdfdpc-wdfdpcenqueue)进行排队。
- 当 UDE 类扩展调用 [*EvtIoCanceledOnQueue*](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_canceled_on_queue) 或 [*EvtRequestCancel*](/windows-hardware/drivers/ddi/wdfrequest/nc-wdfrequest-evt_wdf_request_cancel)时，客户端驱动程序必须在来自调用方的线程或 dpc 的单独 DPC 上完成收到的 URB。 为此，驱动程序必须为其[**URB**](/windows-hardware/drivers/ddi/usb/ns-usb-_urb)队列提供*EvtIoCanceledOnQueue*回调。