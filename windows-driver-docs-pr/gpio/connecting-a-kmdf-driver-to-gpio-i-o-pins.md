---
title: 将 KMDF 驱动程序连接到 GPIO I/O 管脚
description: 外围设备的内核模式驱动程序框架 (KMDF) 驱动程序如何获取 GPIO I/O 资源的说明。
ms.assetid: 02F6431C-7B55-4DFB-9792-4A72F0268C76
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bcf771912ecf322e67b2e6e697b2f73740312e76
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63326165"
---
# <a name="connecting-a-kmdf-driver-to-gpio-io-pins"></a>将 KMDF 驱动程序连接到 GPIO I/O 管脚


GPIO I/O 资源的一个或多个 GPIO 固定配置为数据输入或数据输出。 以物理方式连接到这些引脚的外围设备的驱动程序将获取从操作系统的相应 GPIO I/O 资源。 外围设备驱动程序在此资源中打开的 GPIO 插针的连接，并将 I/O 请求发送到表示此连接的句柄。

下面的代码示例演示外围设备的内核模式驱动程序框架 (KMDF) 驱动程序如何获取 GPIO I/O 资源插即用 (PnP) 管理器分配给该驱动程序的说明。

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

在前面的代码示例中，`DeviceExtension`变量是指向外围设备的设备上下文的指针。 `XyzDrvGetDeviceExtension`函数检索此设备上下文，实现外围设备驱动程序。 此驱动程序之前已注册其[ *EvtDevicePrepareHardware* ](https://msdn.microsoft.com/library/windows/hardware/ff540880)通过调用回调函数[ **WdfDeviceInitSetPnpPowerEventCallbacks**](https://msdn.microsoft.com/library/windows/hardware/ff546135)方法。

下面的代码示例演示如何外围设备驱动程序可以使用它在以前获取的 GPIO 资源说明打开驱动程序的 GPIO I/O 资源的 WDFIOTARGET 句柄的代码示例。

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

在前面的代码示例中，`Device`变量是外围设备的 framework 设备对象的 WDFDEVICE 句柄。 **资源\_中心\_创建\_路径\_FROM\_ID**函数创建包含 GPIO I/O 资源的名称的字符串。 代码示例使用此字符串来按名称打开 GPIO I/O 资源。

外围设备驱动程序获取 GPIO I/O 资源的句柄后，此驱动程序可以发送 I/O 控制请求要从中读取数据或将数据写入到的 GPIO 插针。 此时将打开的 GPIO I/O 资源的驱动程序读取使用[ **IOCTL\_GPIO\_读取\_PIN** ](https://msdn.microsoft.com/library/windows/hardware/hh406483) I/O 控制请求从球瓶的资源中读取数据。 此时将打开的 GPIO I/O 资源的驱动程序将使用写入[ **IOCTL\_GPIO\_编写\_PIN** ](https://msdn.microsoft.com/library/windows/hardware/hh406487) I/O 控制请求，将数据写入到的资源中的球瓶。 下面的代码示例演示如何执行 GPIO 读取或写入操作。

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

在前面的代码示例中，`Data`是指向数据缓冲区的指针`Size`是以字节为单位，此数据缓冲区的大小和`ReadOperation`指示请求的操作是读取 (**TRUE**) 或写 (**FALSE**)。

## <a name="for-more-information"></a>更多相关信息


有关详细信息**IOCTL\_GPIO\_读取\_PIN**请求，包括在请求输出缓冲区中的数据输入 pin 的位的映射，请参阅[ **IOCTL\_GPIO\_读取\_PIN**](https://msdn.microsoft.com/library/windows/hardware/hh406483)。 有关详细信息**IOCTL\_GPIO\_编写\_PIN**请求，包括数据输出插针，将请求输入缓冲区中的位的映射，请参阅[ **IOCTL\_GPIO\_编写\_PIN**](https://msdn.microsoft.com/library/windows/hardware/hh406487)。

有关演示如何编写 GPIO 外围设备驱动程序在内核模式下运行的一个示例驱动程序，请参阅中的 SimDevice 示例驱动程序[GPIO 示例驱动程序](https://go.microsoft.com/fwlink/p/?LinkId=616032)GitHub 上的集合。

 

 




