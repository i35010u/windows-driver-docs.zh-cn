---
title: 将 KMDF 驱动程序连接到 GPIO I/O 管脚
description: 外围设备的内核模式驱动程序框架（KMDF）驱动程序如何获取 GPIO i/o 资源的说明。
ms.assetid: 02F6431C-7B55-4DFB-9792-4A72F0268C76
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 076ada4fa04dde1ef95ad0ac85880b21e97ddbcb
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72825054"
---
# <a name="connecting-a-kmdf-driver-to-gpio-io-pins"></a>将 KMDF 驱动程序连接到 GPIO I/O 管脚


GPIO i/o 资源是配置为数据输入或数据输出的一个或多个 GPIO pin 集。 物理连接到这些 pin 的外围设备的驱动程序从操作系统获取相应的 GPIO i/o 资源。 此资源中的设备驱动程序会打开与 GPIO pin 的连接，并将 i/o 请求发送到表示此连接的句柄。

下面的代码示例演示了外围设备的内核模式驱动程序框架（KMDF）驱动程序如何获取即插即用（PnP）管理器分配给该驱动程序的 GPIO i/o 资源的说明。

```cpp
NTSTATUS
  EvtDevicePrepareHardware(
    _In_ WDFDEVICE Device,
    _In_ WDFCMRESLIST ResourcesRaw,
    _In_ WDFCMRESLIST ResourcesTranslated
    )
{
    int ResourceCount, Index;
    PCM_PARTIAL_RESOURCE_DESCRIPTOR Descriptor;
    XYZ_DEVICE_CONTEXT *DeviceExtension;

    ...

    DeviceExtension = XyzDrvGetDeviceExtension(Device);
    ResourceCount = WdfCmResourceListGetCount(ResourcesTranslated);
    for (Index = 0; Index < ResourceCount; Index += 1) {
        Descriptor = WdfCmResourceListGetDescriptor(ResourcesTranslated, Index);
        switch (Descriptor->Type) {

        //
        // GPIO I/O descriptors
        //

        case CmResourceTypeConnection:

            //
            // Check against expected connection type.
            //

            if ((Descriptor->u.Connection.Class == CM_RESOURCE_CONNECTION_CLASS_GPIO) &&
                (Descriptor->u.Connection.Type == CM_RESOURCE_CONNECTION_TYPE_GPIO_IO)) {

                DeviceExtension->ConnectionId.LowPart = Descriptor->u.Connection.IdLowPart;
                DeviceExtension->ConnectionId.HighPart = Descriptor->u.Connection.IdHighPart;

        ...

}
```

在上面的代码示例中，`DeviceExtension` 变量是指向外围设备的设备上下文的指针。 用于检索此设备上下文的 `XyzDrvGetDeviceExtension` 函数由外围设备驱动程序实现。 此驱动程序以前通过调用[**WdfDeviceInitSetPnpPowerEventCallbacks**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetpnppowereventcallbacks)方法注册了其[*EvtDevicePrepareHardware*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)回调函数。

下面的代码示例演示外围设备驱动程序如何使用在前面的代码示例中获取的 GPIO 资源说明来打开驱动程序 GPIO i/o 资源的 WDFIOTARGET 句柄。

```cpp
NTSTATUS IoRoutine(WDFDEVICE Device, BOOLEAN ReadOperation) 
{
    WDFIOTARGET IoTarget;
    XYZ_DEVICE_CONTEXT *DeviceExtension;
    UNICODE_STRING ReadString;
    WCHAR ReadStringBuffer[100];;
    BOOL DesiredAccess;
    NTSTATUS Status;
    WDF_OBJECT_ATTRIBUTES ObjectAttributes;
    WDF_IO_TARGET_OPEN_PARAMS OpenParams

    DeviceExtension = XyzDrvGetDeviceExtension(Device);
    RtlInitEmptyUnicodeString(&ReadString,
                              ReadStringBuffer,
                              sizeof(ReadStringBuffer));

    Status = RESOURCE_HUB_CREATE_PATH_FROM_ID(&ReadString,
                                              DeviceExtension->ConnectionId.LowPart,
                                              DeviceExtension->ConnectionId.HighPart);

    NT_ASSERT(NT_SUCCESS(Status));

    WDF_OBJECT_ATTRIBUTES_INIT(&ObjectAttributes);
    ObjectAttributes.ParentObject = Device;

    Status = WdfIoTargetCreate(Device, &ObjectAttributes, &IoTarget);
    if (!NT_SUCCESS(Status)) {
        goto IoErrorEnd;
    }   

    if (ReadOperation != FALSE) {
        DesiredAccess = GENERIC_READ;
    } else {
        DesiredAccess = GENERIC_WRITE;
    }

    WDF_IO_TARGET_OPEN_PARAMS_INIT_OPEN_BY_NAME(&OpenParams, ReadString, DesiredAccess);

    Status = WdfIoTargetOpen(IoTarget, &OpenParams);
    if (!NT_SUCCESS(Status)) {
        goto IoErrorEnd;
    }
    ...
```

在上面的代码示例中，`Device` 变量是外围设备的框架设备对象的 WDFDEVICE 句柄。 **资源\_中心\_从\_ID 函数创建\_路径\_** 会创建一个包含 GPIO i/o 资源名称的字符串。 此代码示例使用此字符串按名称打开 GPIO i/o 资源。

在外设驱动程序已获取 GPIO i/o 资源的句柄之后，此驱动程序可以发送 i/o 控制请求，以从 GPIO pin 读取数据或向其写入数据。 为读取打开 GPIO i/o 资源的驱动程序使用[**IOCTL\_GPIO\_读取\_引脚**](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpio/ni-gpio-ioctl_gpio_read_pins)i/o 控制请求，以从资源的 pin 读取数据。 用于打开 GPIO i/o 资源进行写入的驱动程序使用[**IOCTL\_GPIO\_写入\_插针**](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpio/ni-gpio-ioctl_gpio_write_pins)i/o 控制请求，以将数据写入资源中的 pin。 下面的代码示例演示如何执行 GPIO 读取或写入操作。

```cpp
    WDF_OBJECT_ATTRIBUTES RequestAttributes;
    WDF_OBJECT_ATTRIBUTES Attributes;
    WDF_REQUEST_SEND_OPTIONS SendOptions;
    WDFREQUEST IoctlRequest;
    WDFIOTARGET IoTarget;
    WDFMEMORY WdfMemory;
    NTSTATUS Status;

    WDF_OBJECT_ATTRIBUTES_INIT(&RequestAttributes);
    Status = WdfRequestCreate(&RequestAttributes, IoTarget, &IoctlRequest);
    if (!NT_SUCCESS(Status)) {
        goto RwErrorExit;
    }

    //
    // Set up a WDF memory object for the IOCTL request.
    //

    WDF_OBJECT_ATTRIBUTES_INIT(&Attributes);
    Attributes.ParentObject = IoctlRequest;
    Status = WdfMemoryCreatePreallocated(&Attributes, Data, Size, &WdfMemory);
    if (!NT_SUCCESS(Status)) {
        goto RwErrorExit;
    }

    //
    // Format the request.
    //

    if (ReadOperation != FALSE) {
        Status = WdfIoTargetFormatRequestForIoctl(IoTarget,
                                                  IoctlRequest,
                                                  IOCTL_GPIO_READ_PINS,
                                                  NULL,
                                                  0,
                                                  WdfMemory,
                                                  0);

    } else {
        Status = WdfIoTargetFormatRequestForIoctl(IoTarget,
                                                  IoctlRequest,
                                                  IOCTL_GPIO_WRITE_PINS,
                                                  WdfMemory,
                                                  0,
                                                  WdfMemory,
                                                  0);
    }

    if (!NT_SUCCESS(Status)) {
        goto RwErrorExit;
    }

    //
    // Send the request synchronously (with a 60-second time-out).
    //

    WDF_REQUEST_SEND_OPTIONS_INIT(&SendOptions,
                                  WDF_REQUEST_SEND_OPTION_SYNCHRONOUS);
    WDF_REQUEST_SEND_OPTIONS_SET_TIMEOUT(&SendOptions,
                                         WDF_REL_TIMEOUT_IN_SEC(60));

    Status = WdfRequestAllocateTimer(IoctlRequest);
    if (!NT_SUCCESS(Status)) {
        goto RwErrorExit;
    }

    if (!WdfRequestSend(IoctlRequest, IoTarget, &SendOptions)) {
        Status = WdfRequestGetStatus(IoctlRequest);
    }

    ...
```

在上面的代码示例中，`Data` 是指向数据缓冲区的指针，`Size` 是此数据缓冲区的大小（以字节为单位），`ReadOperation` 指示请求的操作是读取（**TRUE**）还是写入（**FALSE**）。

## <a name="for-more-information"></a>有关详细信息


有关**IOCTL\_GPIO 的详细信息\_读取\_插**针请求，包括将数据输入插针映射到请求输出缓冲区中的位，请参阅[**IOCTL\_GPIO\_读取\_的 pin**](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpio/ni-gpio-ioctl_gpio_read_pins)。 若要详细了解**IOCTL\_GPIO\_写入\_pin**请求，包括请求输入缓冲区中的位映射到数据输出插针，请参阅[**IOCTL\_GPIO\_写入\_pin**](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpio/ni-gpio-ioctl_gpio_write_pins)。

有关演示如何编写在内核模式下运行的 GPIO 外设驱动程序的示例驱动程序，请参阅 GitHub 上的[gpio 示例驱动](https://go.microsoft.com/fwlink/p/?LinkId=616032)程序集合中的 SimDevice 示例驱动程序。

 

 




