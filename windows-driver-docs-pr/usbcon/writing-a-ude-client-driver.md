---
Description: 介绍 USB 设备 Emulation(UDE) 类扩展和客户端驱动程序必须为仿真的主机控制器和设备附加到它执行的任务的行为。
title: 编写 UDE 客户端驱动程序
ms.date: 01/07/2019
ms.localizationpriority: medium
ms.openlocfilehash: e06d4acd349f1d132975032c9a4a76bac1e07d93
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366495"
---
# <a name="write-a-ude-client-driver"></a>编写 UDE 客户端驱动程序

**摘要**

- UDE 对象和类扩展和客户端驱动程序使用的句柄。
- 使用功能查询控制器功能和重置控制器创建仿真的主机控制器。
- 创建虚拟的 USB 设备，将其设置为电源管理和数据传输通过终结点。

**适用于：**

- Windows 10

**上次更新时间：**

- 2015 年 11 月

**重要的 API**

- [Emulated USB host controller driver programming reference](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/mt628025(v=vs.85))（模拟 USB 主控制器驱动程序编程参考）

介绍 USB 设备 Emulation(UDE) 类扩展和客户端驱动程序必须为仿真的主机控制器和设备附加到它执行的任务的行为。 它提供有关与每个通过一系列例程和回调函数的类驱动程序和类扩展的进行通信的信息。 它还介绍的功能的客户端驱动程序应实现。

## <a name="before-you-begin"></a>开始之前

- [安装](https://go.microsoft.com/fwlink/p/?LinkID=733614)最新 Windows Driver Kit (WDK) 在开发计算机。 该工具包具有必需的标头文件和库，用于编写 UDE 客户端驱动程序，具体而言，你将需要：
  - 存根 （stub） 库中，(Udecxstub.lib)。 库将转换所做的客户端驱动程序的调用，并将其传递到 UdeCx。
  - 标头文件，Udecx.h。
- 在目标计算机上安装 Windows 10。
- 熟悉 UDE。 请参阅[体系结构：USB 设备 Emulation(UDE)](usb-emulated-device--ude--architecture.md)。
- 了解使用 Windows Driver Foundation (WDF)。 推荐阅读的主题：[使用 Windows Driver Foundation 开发驱动程序]( https://go.microsoft.com/fwlink/p/?LinkId=691676)、 由 Penny Orwick 和 Smith 专家编写。

## <a name="ude-objects-and-handles"></a>UDE 对象和句柄

UDE 类扩展和客户端驱动程序使用特定表示仿真的主机控制器和虚拟设备，包括其终结点和用于在设备和主机之间传输数据的 URBs 的 WDF 对象。 客户端驱动程序请求的对象的创建和对象生存期由类扩展。

- **仿真的主机控制器对象 (WDFDEVICE)**

    表示模拟的主控制器和 UDE 类扩展和客户端驱动程序之间的主要句柄。

- **UDE 设备对象 (UDECXUSBDEVICE)**

    表示虚拟的 USB 设备连接到仿真的主机控制器上的端口。

- **UDE 终结点对象 (UDECXUSBENDPOINT)**

    表示顺序数据管道的 USB 设备。 用于接收软件请求，以发送或接收终结点上的数据。

## <a name="initialize-the-emulated-host-controller"></a>初始化仿真的主机控制器

下面是序列的客户端驱动程序在其中检索仿真的主机控制器的 WDFDEVICE 句柄的摘要。 我们建议，该驱动程序中执行这些任务及其[ *EvtDriverDeviceAdd* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)回调函数。

1. 调用[ **UdecxInitializeWdfDeviceInit** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxwdfdevice/nf-udecxwdfdevice-udecxinitializewdfdeviceinit)由传递到引用[WDFDEVICE\_INIT](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfdevice_init)框架传递。
2. 初始化[WDFDEVICE\_INIT](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfdevice_init)结构与安装程序的信息，以便此设备看起来类似于其他 USB 主控制器。 例如分配 FDO 名称和符号链接，向 Microsoft 提供 GUID 注册设备接口\_DEVINTERFACE\_USB\_主机\_控制器 GUID 作为设备接口的 GUID，以便应用程序可以打开到设备的句柄。
3. 调用[ **WdfDeviceCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicecreate)创建 framework 设备对象。
4. 调用[ **UdecxWdfDeviceAddUsbDeviceEmulation** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxwdfdevice/nf-udecxwdfdevice-udecxwdfdeviceaddusbdeviceemulation)并注册客户端驱动程序的回调函数。

    以下是与主机控制器对象中，相关联的回调函数调用的 UDE 类扩展。 这些函数必须由客户端驱动程序实现。

    [*EVT\_UDECX\_WDF\_设备\_查询\_USB\_功能*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxwdfdevice/nc-udecxwdfdevice-evt_udecx_wdf_device_query_usb_capability)  
    确定在客户端驱动程序必须报告至类扩展的主机控制器支持的功能。

    [*EVT\_UDECX\_WDF\_DEVICE\_RESET*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxwdfdevice/nc-udecxwdfdevice-evt_udecx_wdf_device_reset)  
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


## <a name="handle-user-mode-ioctl-requests-sent-to-the-host-controller"></a>处理用户模式下 IOCTL 请求发送到主控制器

在初始化期间，UDE 客户端驱动程序将公开 GUID\_DEVINTERFACE\_USB\_主机\_控制器设备接口的 GUID。 这使驱动程序的应用程序将设备句柄打开使用该 GUID 从接收 IOCTL 请求。 IOCTL 控制代码的列表，请参阅[应用程序和服务的 USB Ioctl](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540046(v=vs.85)#um-ioctl)与设备接口的 GUID:GUID\_DEVINTERFACE\_USB\_主机\_控制器。

若要处理这些请求，客户端驱动程序注册[ *EvtIoDeviceControl* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_device_control)事件回调。 在实现中，而不是处理请求，该驱动程序可以选择将请求转发到 UDE 类扩展插件进行处理。 若要将请求转发，驱动程序必须调用[ **UdecxWdfDeviceTryHandleUserIoctl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxwdfdevice/nf-udecxwdfdevice-udecxwdfdevicetryhandleuserioctl)。 如果收到的 IOCTL 控制代码对应于标准的请求，如检索设备描述符类扩展处理并已成功完成请求。 在这种情况下， **UdecxWdfDeviceTryHandleUserIoctl**完成时返回的值为 TRUE。 否则，调用会返回 FALSE，并且该驱动程序必须确定如何完成该请求。 在最简单的实现中，该驱动程序可以通过调用完成并返回相应的故障代码请求[ **WdfRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestcomplete)。

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

## <a name="report-the-capabilities-of-the-host-controller"></a>报告的主控制器的功能


上层驱动程序可以使用 USB 主控制器的功能之前，驱动程序必须确定控制器是否支持这些功能。 驱动程序通过调用做出此类查询[ **WdfUsbTargetDeviceQueryUsbCapability** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicequeryusbcapability)并[ **USBD\_QueryUsbCapability** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/hh406230(v=vs.85)). 这些调用转发到 USB 设备 Emulation(UDE) 类扩展。 在收到请求，此类扩展调用客户端驱动程序[ *EVT\_UDECX\_WDF\_设备\_查询\_USB\_功能*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxwdfdevice/nc-udecxwdfdevice-evt_udecx_wdf_device_query_usb_capability)实现。 此调用后，才[ *EvtDriverDeviceAdd* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)完成后，通常是在[ *EvtDevicePrepareHardware* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)和不之后[*EvtDeviceReleaseHardware*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_release_hardware)。 这是回调函数是必需。

在实现中，客户端驱动程序必须报告它是否支持请求的功能。 某些功能不受 UDE 如静态流。

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

## <a name="create-a-virtual-usb-device"></a>创建一个虚拟的 USB 设备

虚拟的 USB 设备的行为类似于 USB 设备。 它将支持具有多个接口配置和每个接口支持备用的设置。 每个设置可以具有一个用于数据传输的更多终结点。 （设备、 配置、 接口、 终结点） 的所有描述符都设置 UDE 客户端驱动程序中，以便设备可以报告类似于实际的 USB 设备的信息。

> [!NOTE]
> UDE 客户端驱动程序不支持外部中心

下面是序列的客户端驱动程序在其中创建 UDE 设备对象的 UDECXUSBDEVICE 句柄的摘要。 该驱动程序必须执行这些步骤之后它已检索仿真的主机控制器 WDFDEVICE 句柄。 我们建议，该驱动程序中执行这些任务及其[ *EvtDriverDeviceAdd* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)回调函数。

1. 调用[ **UdecxUsbDeviceInitAllocate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxusbdevice/nf-udecxusbdevice-udecxusbdeviceinitallocate)以获得到创建该设备所需的初始化参数的指针。 此结构分配了 UDE 类扩展。
2. 通过设置成员的注册事件回调函数[ **UDECX\_USB\_设备\_状态\_更改\_回调**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxusbdevice/ns-udecxusbdevice-_udecx_usb_device_state_change_callbacks)和然后调用[ **UdecxUsbDeviceInitSetStateChangeCallbacks**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxusbdevice/nf-udecxusbdevice-udecxusbdeviceinitsetstatechangecallbacks)。 以下是 UDE 设备对象时，相关联的回调函数调用的 UDE 类扩展。

    若要创建或配置终结点的客户端驱动程序通过实现这些函数。

   - [*EVT\_UDECX\_USB\_DEVICE\_DEFAULT\_ENDPOINT\_ADD*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxusbdevice/nc-udecxusbdevice-evt_udecx_usb_device_default_endpoint_add)
   - [*EVT\_UDECX\_USB\_DEVICE\_ENDPOINT\_ADD*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxusbdevice/nc-udecxusbdevice-evt_udecx_usb_device_endpoint_add)
   - [*EVT\_UDECX\_USB\_DEVICE\_ENDPOINTS\_CONFIGURE*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxusbdevice/nc-udecxusbdevice-evt_udecx_usb_device_endpoints_configure)

     <!-- -->

   - [*EVT\_UDECX\_USB\_DEVICE\_D0\_ENTRY*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxusbdevice/nc-udecxusbdevice-evt_udecx_usb_device_d0_entry)
   - [*EVT\_UDECX\_USB\_DEVICE\_D0\_EXIT*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxusbdevice/nc-udecxusbdevice-evt_udecx_usb_device_d0_exit)
   - [*EVT\_UDECX\_USB\_DEVICE\_SET\_FUNCTION\_SUSPEND\_AND\_WAKE*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxusbdevice/nc-udecxusbdevice-evt_udecx_usb_device_set_function_suspend_and_wake)

3. 调用[ **UdecxUsbDeviceInitSetSpeed** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxusbdevice/nf-udecxusbdevice-udecxusbdeviceinitsetspeed)若要设置 USB 设备的速度以及设备、 USB 2.0 或 SuperSpeed 设备的类型。
4. 调用[ **UdecxUsbDeviceInitSetEndpointsType** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxusbdevice/nf-udecxusbdevice-udecxusbdeviceinitsetendpointstype)指定终结点设备支持的类型： 简单或动态。 如果客户端驱动程序中选择创建简单终结点，该驱动程序必须在插入设备之前创建终结点的所有对象。 每个接口，设备必须具有只有一个配置和只有一种接口设置。 在动态终结点的情况下，驱动程序可以创建在终结点接收时插入该设备之后，任何时候[ *EVT\_UDECX\_USB\_设备\_的终结点\_配置*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxusbdevice/nc-udecxusbdevice-evt_udecx_usb_device_endpoints_configure)事件回调。 请参阅[创建动态终结点](#create-dynamic-endpoints)。
5. 调用任何一种方法来将必要的描述符添加到设备。

   - [**UdecxUsbDeviceInitAddDescriptor**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxusbdevice/nf-udecxusbdevice-udecxusbdeviceinitadddescriptor)
   - [**UdecxUsbDeviceInitAddDescriptorWithIndex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxusbdevice/nf-udecxusbdevice-udecxusbdeviceinitadddescriptorwithindex)
   - [**UdecxUsbDeviceInitAddStringDescriptor**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxusbdevice/nf-udecxusbdevice-udecxusbdeviceinitaddstringdescriptor)
   - [**UdecxUsbDeviceInitAddStringDescriptorRaw**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxusbdevice/nf-udecxusbdevice-udecxusbdeviceinitaddstringdescriptorraw)

     如果 UDE 类扩展插件接收在初始化期间通过使用上述方法之一提供客户端驱动程序的标准描述符的请求，此类扩展会自动完成请求。 类扩展不会不该请求转发到客户端驱动程序。 此设计可降低该驱动程序必须处理控制请求的请求数。 此外，它也不需要的驱动程序来实现需要安装数据包的大量分析和处理的描述符逻辑**并将 wLength**并**TransferBufferLength**正确。 此列表包含标准的请求。 客户端驱动程序不需要检查这些请求 （仅在前面的方法调用添加描述符）：

   - USB\_请求\_获取\_描述符
   - USB\_REQUEST\_SET\_CONFIGURATION
   - USB\_REQUEST\_SET\_INTERFACE
   - USB\_REQUEST\_SET\_ADDRESS
   - USB\_请求\_设置\_功能
   - USB\_功能\_函数\_挂起
   - USB\_FEATURE\_REMOTE\_WAKEUP
   - USB\_请求\_清除\_功能
   - USB\_功能\_终结点\_停滞
   - USB\_REQUEST\_SET\_SEL
   - USB\_请求\_ISOCH\_延迟

     但是，接口，特定于类或供应商定义描述符的请求，UDE 类扩展将其转发到客户端驱动程序。 该驱动程序必须处理这些 GET\_描述符请求。

6. 调用[ **UdecxUsbDeviceCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxusbdevice/nf-udecxusbdevice-udecxusbdevicecreate)创建 UDE 设备对象并检索 UDECXUSBDEVICE 句柄。
7. 通过调用创建静态终结点[ **UdecxUsbEndpointCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxusbendpoint/nf-udecxusbendpoint-udecxusbendpointcreate)。 请参阅[创建简单终结点](#create-simple-endpoints)。
8. 调用[ **UdecxUsbDevicePlugIn** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxusbdevice/nf-udecxusbdevice-udecxusbdeviceplugin)以指示 UDE 类扩展到附加设备，并可接收终结点上的 I/O 请求。 此调用后，此类扩展还可以调用终结点和 USB 设备上的回调函数。
    **请注意**USB 设备需要在运行时中删除，如果客户端驱动程序可以调用[ **UdecxUsbDevicePlugOutAndDelete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxusbdevice/nf-udecxusbdevice-udecxusbdeviceplugoutanddelete)。 如果要使用的设备驱动程序，它必须创建它通过调用[ **UdecxUsbDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxusbdevice/nf-udecxusbdevice-udecxusbdevicecreate)。

在此示例中，假定描述符声明为全局变量，声明只是作为示例 HID 设备的如下所示：

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

下面是的示例中的客户端驱动程序指定初始化参数通过注册回调函数以及设置设备的速度、 指示类型的终结点，最后设置某些设备描述符。

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


UDE 类扩展调用客户端驱动程序的回调函数，当它收到的请求将发送设备以较低的电源状态，或者将恢复到工作状态。 这些回调函数是必需的 USB 设备的支持。 客户端驱动程序已通过其实现注册到上一个调用中[ **UdecxUsbDeviceInitSetStateChangeCallbacks**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxusbdevice/nf-udecxusbdevice-udecxusbdeviceinitsetstatechangecallbacks)。

有关详细信息，请参阅[USB 设备的电源状态](comparing-usb-device-states-to-wdm-device-states.md)。

[*EVT\_UDECX\_USB\_DEVICE\_D0\_ENTRY*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxusbdevice/nc-udecxusbdevice-evt_udecx_usb_device_d0_entry)  
客户端驱动程序将转换为 D0 状态 Dx 状态的设备。

[*EVT\_UDECX\_USB\_DEVICE\_D0\_EXIT*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxusbdevice/nc-udecxusbdevice-evt_udecx_usb_device_d0_exit)  
客户端驱动程序将转换为 Dx 状态 D0 状态的设备。

[*EVT\_UDECX\_USB\_DEVICE\_SET\_FUNCTION\_SUSPEND\_AND\_WAKE*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxusbdevice/nc-udecxusbdevice-evt_udecx_usb_device_set_function_suspend_and_wake)  
客户端驱动程序更改虚拟的 USB 3.0 设备的指定接口的函数状态。

USB 3.0 设备允许各个函数进入节能状态。 每个函数都还能够发送唤醒信号。 UDE 类扩展通知客户端驱动程序通过调用[ *EVT\_UDECX\_USB\_设备\_设置\_函数\_挂起\_AND\_唤醒*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxusbdevice/nc-udecxusbdevice-evt_udecx_usb_device_set_function_suspend_and_wake)。 此事件指示函数电源状态更改，并通知该函数可以是否从新的状态中唤醒的客户端驱动程序。 在函数中，类扩展将传递唤醒函数接口的数。
客户端驱动程序可以模拟唤醒低链接电源状态，函数从其自己暂停，请虚拟 USB 设备启动和 / 或的操作。 对于 USB 2.0 设备，该驱动程序必须调用[ **UdecxUsbDeviceSignalWake**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxusbdevice/nf-udecxusbdevice-udecxusbdevicesignalwake)，如果启用唤醒设备中的最新驱动程序[ *EVT\_UDECX\_USB\_设备\_D0\_退出*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxusbdevice/nc-udecxusbdevice-evt_udecx_usb_device_d0_exit)。 对于 USB 3.0 设备驱动程序必须调用[ **UdecxUsbDeviceSignalFunctionWake** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxusbdevice/nf-udecxusbdevice-udecxusbdevicesignalfunctionwake) USB 3.0 唤醒功能是每个函数。 如果整个设备在低功耗状态，或输入这种状态**UdecxUsbDeviceSignalFunctionWake**唤醒设备。

## <a name="create-simple-endpoints"></a>创建简单终结点


客户端驱动程序创建 UDE 终结点对象，以处理数据传输到和从 USB 设备。 驱动程序创建简单终结点之后创建 UDE 设备和之前报告的设备，如接通电源。

下面是序列的客户端驱动程序在其中创建 UDE 终结点对象的 UDECXUSBENDPOINT 句柄的摘要。 检索虚拟的 USB 设备的 UDECXUSBDEVICE 句柄后，该驱动程序必须执行这些步骤。 我们建议，该驱动程序中执行这些任务及其[ *EvtDriverDeviceAdd* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)回调函数。

1. 调用[ **UdecxUsbSimpleEndpointInitAllocate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxusbendpoint/nf-udecxusbendpoint-udecxusbsimpleendpointinitallocate)以获得到分配的类扩展的初始化参数的指针。
2. 调用[ **UdecxUsbEndpointInitSetEndpointAddress** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxusbendpoint/nf-udecxusbendpoint-udecxusbendpointinitsetendpointaddress)中的初始化参数设置终结点地址。
3. 调用[ **UdecxUsbEndpointInitSetCallbacks** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxusbendpoint/nf-udecxusbendpoint-udecxusbendpointinitsetcallbacks)注册客户端驱动程序实现回调函数。

    这些函数的实现客户端驱动程序来处理队列和终结点上的请求。

    [*EVT\_UDECX\_USB\_ENDPOINT\_RESET*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxusbendpoint/nc-udecxusbendpoint-evt_udecx_usb_endpoint_reset)  
    重置虚拟的 USB 设备的终结点。

    [*EVT\_UDECX\_USB\_ENDPOINT\_START*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxusbendpoint/nc-udecxusbendpoint-evt_udecx_usb_endpoint_start)  
    可选。 开始处理 I/O 请求

    [*EVT\_UDECX\_USB\_终结点\_清除*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxusbendpoint/nc-udecxusbendpoint-evt_udecx_usb_endpoint_purge)  
    可选。 停止队列对终结点的队列的 I/O 请求并取消未处理的请求。

4. 调用[ **UdecxUsbEndpointCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxusbendpoint/nf-udecxusbendpoint-udecxusbendpointcreate)以创建终结点对象并检索 UDECXUSBENDPOINT 句柄。
5. 调用[ **UdecxUsbEndpointSetWdfIoQueue** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxusbendpoint/nf-udecxusbendpoint-udecxusbendpointsetwdfioqueue)将 framework 队列对象与终结点相关联。 如果适用，它可以设置要在队列设置适当的属性的 WDF 父对象的终结点对象。

    每个终结点对象以处理传输请求具有 framework 队列对象。 对于类扩展插件接收每个传输请求，该队列 framework 请求对象。 队列的状态 （启动、 清除） 是由 UDE 类扩展和客户端驱动程序不得更改该状态。 每个请求对象包含 USB 请求块 ([**URB**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_urb))，其中包含传输的详细信息。

在此示例中，客户端驱动程序创建默认控制终结点。

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


客户端驱动程序可以在 UDE 类扩展的请求 （代表的中心驱动程序和客户端驱动程序） 时创建动态终结点。 类扩展可以通过调用这些回调函数的任何请求：

[*EVT\_UDECX\_USB\_DEVICE\_DEFAULT\_ENDPOINT\_ADD*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxusbdevice/nc-udecxusbdevice-evt_udecx_usb_device_default_endpoint_add)  
客户端驱动程序创建默认的控制终结点 （终结点 0）

[*EVT\_UDECX\_USB\_DEVICE\_ENDPOINT\_ADD*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxusbdevice/nc-udecxusbdevice-evt_udecx_usb_device_endpoint_add)  
客户端驱动程序创建动态终结点。

[*EVT\_UDECX\_USB\_DEVICE\_ENDPOINTS\_CONFIGURE*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxusbdevice/nc-udecxusbdevice-evt_udecx_usb_device_endpoints_configure)  
客户端驱动程序通过选择一项备用设置、 禁用当前的终结点，或添加动态终结点更改配置。

客户端驱动程序在其调用期间注册上述回调[ **UdecxUsbDeviceInitSetStateChangeCallbacks**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxusbdevice/nf-udecxusbdevice-udecxusbdeviceinitsetstatechangecallbacks)。 请参阅创建[虚拟 USB 设备](#create-a-virtual-usb-device)。
此机制允许客户端驱动程序，以动态更改的 USB 配置和设备上的接口设置。 例如，当需要终结点对象，或必须发布现有终结点对象，则类扩展将调用[ *EVT\_UDECX\_USB\_设备\_的终结点\_配置*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxusbdevice/nc-udecxusbdevice-evt_udecx_usb_device_endpoints_configure)。

下面是序列的客户端驱动程序在其中创建它的实现的回调函数中的终结点对象的 UDECXUSBENDPOINT 句柄的摘要。

1. 调用[ **UdecxUsbEndpointInitSetEndpointAddress** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxusbendpoint/nf-udecxusbendpoint-udecxusbendpointinitsetendpointaddress)中的初始化参数设置终结点地址。
2. 调用[ **UdecxUsbEndpointInitSetCallbacks** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxusbendpoint/nf-udecxusbendpoint-udecxusbendpointinitsetcallbacks)注册客户端驱动程序实现回调函数。 类似于简单的终结点，该驱动程序可以注册这些回调函数：
    - [*EVT\_UDECX\_USB\_终结点\_重置*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxusbendpoint/nc-udecxusbendpoint-evt_udecx_usb_endpoint_reset) （必需）。
    - [*EVT\_UDECX\_USB\_ENDPOINT\_START*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxusbendpoint/nc-udecxusbendpoint-evt_udecx_usb_endpoint_start)
    - [*EVT\_UDECX\_USB\_终结点\_清除*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxusbendpoint/nc-udecxusbendpoint-evt_udecx_usb_endpoint_purge)

3. 调用[ **UdecxUsbEndpointCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxusbendpoint/nf-udecxusbendpoint-udecxusbendpointcreate)以创建终结点对象并检索 UDECXUSBENDPOINT 句柄。
4. 调用[ **UdecxUsbEndpointSetWdfIoQueue** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxusbendpoint/nf-udecxusbendpoint-udecxusbendpointsetwdfioqueue)将 framework 队列对象与终结点相关联。

在此示例实现中，客户端驱动程序创建动态默认控制终结点。

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

## <a name="perform-error-recovery-by-resetting-an-endpoint"></a>通过重置终结点执行错误恢复


有时，数据传输可能会因各种原因，例如终结点中的停止条件失败。 在故障转移的情况下在终结点无法处理请求，直到清除错误条件。 当 UDE 类扩展遇到失败的数据传输时，它将调用客户端驱动程序[ *EVT\_UDECX\_USB\_终结点\_重置*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxusbendpoint/nc-udecxusbendpoint-evt_udecx_usb_endpoint_reset)回调函数，该对的上一个调用中注册的驱动程序函数[ **UdecxUsbEndpointInitSetCallbacks**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxusbendpoint/nf-udecxusbendpoint-udecxusbendpointinitsetcallbacks)。 在实现中，该驱动程序可以选择清除管道的停止状态和执行其他必要的步骤，以清除错误条件。

此调用是异步的。 客户端与重置操作完成之后，驱动程序必须通过调用完成并返回相应的故障代码请求[ **WdfRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestcomplete)。 该调用会通知 UDE 客户端扩展的状态重置操作已完成。

**请注意**错误恢复所必需的复杂解决方案时，客户端驱动程序已重置主机控制器的选项。 可以在中实现此逻辑[ *EVT\_UDECX\_WDF\_设备\_重置*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxwdfdevice/nc-udecxwdfdevice-evt_udecx_wdf_device_reset)驱动程序在其已注册的回调函数[**UdecxWdfDeviceAddUsbDeviceEmulation** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxwdfdevice/nf-udecxwdfdevice-udecxwdfdeviceaddusbdeviceemulation)调用。 如果适用，驱动程序可以重置主机控制器和所有下游设备。 如果客户端驱动程序并不需要重置控制器，但重置所有下游设备，必须指定驱动程序**UdeWdfDeviceResetActionResetEachUsbDevice**在注册过程中的配置参数中。 在这种情况下，此类扩展调用*EVT\_UDECX\_WDF\_设备\_重置*每个连接的设备。

## <a name="implement-queue-state-management"></a>实现队列的状态管理

UDE 类扩展由管理与 UDE 终结点对象相关联的 framework 队列对象的状态。 但是，如果客户端驱动程序将从终结点队列的请求转发到其他内部队列中，客户端必须实现逻辑以应对终结点的 I/O 流中的变化。 这些回调函数中注册到[ **UdecxUsbEndpointInitSetCallbacks**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxusbendpoint/nf-udecxusbendpoint-udecxusbendpointinitsetcallbacks)。

### <a name="endpoint-purge-operation"></a>终结点清除操作

与每个终结点的一个队列 UDE 客户端驱动程序可以实现[ *EVT\_UDECX\_USB\_终结点\_清除*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxusbendpoint/nc-udecxusbendpoint-evt_udecx_usb_endpoint_purge) ，在此示例中所示：

在中[ *EVT\_UDECX\_USB\_终结点\_清除*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxusbendpoint/nc-udecxusbendpoint-evt_udecx_usb_endpoint_purge)实现中，客户端驱动程序所需确保从转发的所有 i/o 操作终结点的队列已完成，并且该新转发的 I/O 也将失败，直到客户端驱动程序[ *EVT\_UDECX\_USB\_终结点\_开始*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxusbendpoint/nc-udecxusbendpoint-evt_udecx_usb_endpoint_start)调用。 通过调用满足这些要求[ **UdecxUsbEndpointPurgeComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxusbendpoint/nf-udecxusbendpoint-udecxusbendpointpurgecomplete)、 这确保所有转发 I/O 完成和失败的未来转发 I/O。

### <a name="endpoint-start-operation"></a>终结点启动操作

在中[ *EVT\_UDECX\_USB\_终结点\_启动*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxusbendpoint/nc-udecxusbendpoint-evt_udecx_usb_endpoint_start)实现中，客户端驱动程序所需开始处理 I/O 上的终结点队列，以及接收终结点转发的 I/O 的任何队列。 创建一个终结点后，它不接收任何 I/O 直到此回调函数返回后。 此回调返回后的处理 I/O 的状态，终结点[ *EVT\_UDECX\_USB\_终结点\_清除*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxusbendpoint/nc-udecxusbendpoint-evt_udecx_usb_endpoint_purge)完成。


## <a name="handling-data-transfer-requests-urbs"></a>处理数据的传输请求 (URBs)


若要处理 USB I/O 请求发送到客户端设备的终结点，截获[EVT_WDF_IO_QUEUE_IO_INTERNAL_DEVICE_CONTROL](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_internal_device_control)上与使用的队列对象的回拨[ **UdecxUsbEndpointInitSetCallbacks** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxusbendpoint/nf-udecxusbendpoint-udecxusbendpointinitsetcallbacks)时将队列与终结点相关联。 在该回调中处理的 I/O [IOCTL\_内部\_USB\_提交\_URB](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbioctl/ni-usbioctl-ioctl_internal_usb_submit_urb) IoControlCode (请参阅下面的示例代码[URB 处理方法](#urb-handling-methods)).


## <a name="urb-handling-methods"></a>URB 处理方法


作为一部分的处理通过 URBs [IOCTL\_内部\_USB\_提交\_URB](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbioctl/ni-usbioctl-ioctl_internal_usb_submit_urb) UDE 客户端驱动程序可以与虚拟设备上的终结点关联的队列，获取指向的指针可以使用这些方法的传输的 I/O 请求的缓冲区：

这些函数的实现客户端驱动程序来处理队列和终结点上的请求。

[**UdecxUrbRetrieveControlSetupPacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxurb/nf-udecxurb-udecxurbretrievecontrolsetuppacket)  
从指定的框架请求对象中检索 USB 控制安装数据包。

[**UdecxUrbRetrieveBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxurb/nf-udecxurb-udecxurbretrievebuffer)  
从指定的框架请求对象发送到终结点队列中检索 URB 的传输缓冲区。

[**UdecxUrbSetBytesCompleted**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxurb/nf-udecxurb-udecxurbsetbytescompleted)  
设置为包含在一个框架请求对象 URB 传输的字节数。

[**UdecxUrbComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxurb/nf-udecxurb-udecxurbcomplete)  
完成 URB 请求使用的特定于 USB 的完成状态代码。

[**UdecxUrbCompleteWithNtStatus**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxurb/nf-udecxurb-udecxurbcompletewithntstatus)  
完成并返回 NTSTATUS 代码 URB 请求。

下面是典型的 USB 出传输 URB 的处理的 I/O 流。

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

客户端驱动程序可以完成在单独的与 DPC 的 I/O 请求。 遵循以下最佳实践：

- 若要确保与现有的 USB 驱动程序的兼容性，UDE 客户端必须调用[ **WdfRequestComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestcomplete)在调度\_级别。
- 如果[ **URB** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_urb)已添加到终结点的队列和驱动程序开始调用驱动程序的线程或 DPC，请求同步处理必须以同步方式完成。 单独 DPC 是必需的这个目的，该驱动程序通过调用排队[ **WdfDpcEnqueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdpc/nf-wdfdpc-wdfdpcenqueue)。
- 当 UDE 类扩展调用[ *EvtIoCanceledOnQueue* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_canceled_on_queue)或[ *EvtRequestCancel*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nc-wdfrequest-evt_wdf_request_cancel)，必须完成客户端驱动程序从调用方的线程或 DPC，接收到 URB 单独 DPC 上。 若要执行此操作，该驱动程序必须提供*EvtIoCanceledOnQueue*回调其[ **URB** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_urb)队列。
