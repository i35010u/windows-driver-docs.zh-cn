---
description: USB 设备以一系列称为 USB 配置的接口的形式公开其功能。
title: USB 配置描述符
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 957d00986ce61bfeb086f4c1c2d7a0edc8045d14
ms.sourcegitcommit: 937974aa9bbe0262a7ffe9631593fab48c4e7492
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/11/2020
ms.locfileid: "90010005"
---
# <a name="usb-configuration-descriptors"></a>USB 配置描述符


USB 设备以一系列称为 USB 配置的接口的形式公开其功能。 每个接口都由一个或多个备用设置组成，每个备用设置由一组终结点组成。 本主题介绍与 USB 配置相关的各种描述符。

配置描述符中介绍了 USB 配置 (参阅 [**usb \_ 配置 \_ 描述符**](/windows-hardware/drivers/ddi/usbspec/ns-usbspec-_usb_configuration_descriptor) 结构) 。 配置描述符包含有关配置及其接口、备用设置及其终结点的信息。 [**USB \_ 接口 \_ 描述符**](/windows-hardware/drivers/ddi/usbspec/ns-usbspec-_usb_interface_descriptor)结构中介绍了每个接口描述符或替代设置。 在配置中，每个接口描述符在内存中后跟接口和备用设置的所有终结点说明符。 每个终结点描述符存储在 [**USB \_ 终结点 \_ 描述符**](/windows-hardware/drivers/ddi/usbspec/ns-usbspec-_usb_endpoint_descriptor) 结构中。

例如，请考虑 [Usb 设备布局](usb-device-layout.md)中所述的 usb 网络摄像机设备。 该设备支持具有两个接口的配置，第一个接口 (索引 0) 支持两个备用设置。

以下示例显示了 USB 网络摄像机设备的配置描述符：

``` syntax
Configuration Descriptor:
wTotalLength:         0x02CA
bNumInterfaces:       0x02
bConfigurationValue:  0x01
iConfiguration:       0x00
bmAttributes:         0x80 (Bus Powered )
MaxPower:             0xFA (500 mA)
```

**BConfigurationValue**字段指示设备固件中定义的配置的编号。 客户端驱动程序使用该数字值来选择活动配置。 有关 [usb 设备配置](configuring-usb-devices.md)的详细信息，请参阅 [如何为 Usb 设备选择配置](how-to-select-a-configuration-for-a-usb-device.md)。 USB 配置还指示某些电源特征。 **BmAttributes**包含一个位掩码，该位掩码指示配置是否支持远程唤醒功能，以及设备是由总线供电还是自供电。 " **MaxPower** " 字段指定设备在总线供电时可以从主机中抽取) 的最大电源 (。 该配置描述符还表明了设备支持 (**bNumInterfaces**) 的接口总数。

以下示例显示了用于网络摄像机设备的接口0的备用设置0的接口描述符：

``` syntax
Interface Descriptor:
bInterfaceNumber:     0x00
bAlternateSetting:    0x00
bNumEndpoints:        0x01
bInterfaceClass:      0x0E
bInterfaceSubClass:   0x02
bInterfaceProtocol:   0x00
iInterface:           0x02
0x0409: "Microsoft LifeCam VX-5000"
0x0409: "Microsoft LifeCam VX-5000"
```

在前面的示例中，请注意 **bInterfaceNumber** 和 **bAlternateSetting** 字段的值。 这些字段包含索引值，客户端驱动程序使用这些值来激活接口及其备用设置之一。 对于激活，驱动程序会向 USB 驱动程序堆栈发送一个选择接口请求。 然后，驱动程序堆栈生成标准控制请求 (集接口) 并将其发送到设备。 请注意 " **bInterfaceClass** " 字段。 接口描述符或它的任何备用设置的描述符指定类代码、子类和协议。 0x0E 的值指示接口适用于视频设备类。 另外，请注意 **iInterface** 字段。 该值指示在接口描述符后面追加了两个字符串说明符。 字符串描述符包含在设备枚举过程中用来标识功能的 Unicode 说明。 有关字符串描述符的详细信息，请参阅 [USB 字符串描述符](usb-string-descriptors.md)。

接口中的每个终结点都描述了设备的单个输入或输出流。 支持不同类型的函数的流的设备有多个接口。 支持多个与函数相关的流的设备可支持单个接口上的多个终结点。

除了默认终结点) 以外，所有类型的终结 (点都必须提供终结点描述符，以便主机可以获取有关终结点的信息。 终结点描述符包含信息，例如其地址、类型、方向和终结点可以处理的数据量。 传输到终结点的数据基于该信息。

以下示例显示了网络摄像机设备的终结点描述符：

``` syntax
Endpoint Descriptor:
bEndpointAddress:   0x82  IN
bmAttributes:       0x01
wMaxPacketSize:     0x0080 (128)
bInterval:          0x01
```

**BEndpointAddress**字段指定包含终结点号的唯一终结点地址 (位 3. 0) 和终结点 (第7位) 的方向。 通过读取前面的示例中的这些值，可以确定该描述符在终结点（其终结点号为2）中进行了说明。 **BmAttributes**特性指示终结点类型为 "同步"。 **WMaxPacketSizefield**指示终结点可以在单个事务中发送或接收的最大字节数。 第12位. 11 表示每个 microframe 可发送的事务总数。 **BInterval**指示终结点可以发送或接收数据的频率。

## <a name="how-to-get-the-configuration-descriptor"></a>如何获取配置描述符


该配置描述符是通过标准设备请求 (获取描述符) 从设备获取的 \_ ，它作为 USB 驱动程序堆栈的控件传输发送。 USB 客户端驱动程序可以通过以下方式之一来启动请求：

- 如果设备仅支持一个配置，最简单的方法是调用框架提供的 [**WdfUsbTargetDeviceRetrieveConfigDescriptor**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdeviceretrieveconfigdescriptor) 方法。
- 对于支持多个配置的设备，如果客户端驱动程序想要获取除第一个配置之外的其他配置描述符，则驱动程序必须提交 URB。 若要提交 URB，驱动程序必须分配和格式，然后将 URB 提交到 USB 驱动程序堆栈。

  若要分配 URB，客户端驱动程序必须调用 [**WdfUsbTargetDeviceCreateUrb**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicecreateurb) 方法。 方法接收指向 USB 驱动程序堆栈所分配的 URB 的指针。

  若要设置 URB 的格式，客户端驱动程序可以使用 [**UsbBuildGetDescriptorRequest**](/previous-versions/ff538943(v=vs.85)) 宏。 宏在 URB 中设置所有必要的信息，如要为其检索描述符的设备定义的配置编号。 URB 函数设置为 URB \_ 函数 \_ GET \_ 描述符 \_ FROM \_ DEVICE (参阅[** \_ URB \_ CONTROL \_ 描述符 \_ REQUEST**](/windows-hardware/drivers/ddi/usb/ns-usb-_urb_control_descriptor_request)) ，将描述符的类型设置为 USB \_ 配置 \_ 描述符 \_ 类型。 通过使用 URB 中包含的信息，USB 驱动程序堆栈生成标准控制请求并将其发送到设备。

  若要提交 URB，客户端驱动程序必须使用 WDF request 对象。 若要以异步方式将请求对象发送到 USB 驱动程序堆栈，驱动程序必须调用 [**WdfRequestSend**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestsend)方法。 若要同步发送它，请调用 [**WdfUsbTargetDeviceSendUrbSynchronously**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicesendurbsynchronously) 方法。

  <strong>Wdm 驱动程序： * * Windows 驱动模型 (WDM) 客户端驱动程序只能通过提交 URB 来获取该配置描述符。若要分配 URB，驱动程序必须调用 [</strong> USBD \_ UrbAllocate <strong>](<https://msdn.microsoft.com/library/windows/hardware/hh406250>) 例程。若要设置 URB 的格式，驱动程序必须调用 [</strong> UsbBuildGetDescriptorRequest * *](<https://msdn.microsoft.com/library/windows/hardware/ff538943>) 宏。 若要提交 URB，驱动程序必须将 URB 与 IRP 相关联，并将 IRP 提交到 USB 驱动程序堆栈。 有关详细信息，请参阅 [如何提交 URB](send-requests-to-the-usb-driver-stack.md)。

在 USB 配置中，接口的数量及其备用设置是可变的。 因此，很难预测保存配置描述符所需的缓冲区大小。 客户端驱动程序必须在两个步骤中收集所有这些信息。 首先，确定保存所有配置描述符所需的缓冲区大小，然后发出请求来检索整个描述符。 客户端驱动程序可以通过下列方式之一获得大小：

**若要通过调用 WdfUsbTargetDeviceRetrieveConfigDescriptor 获取配置描述符，请执行以下步骤：**

1.  通过调用 [**WdfUsbTargetDeviceRetrieveConfigDescriptor**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdeviceretrieveconfigdescriptor)获取保存所有配置信息所需的缓冲区大小。 驱动程序必须在缓冲区中传递 NULL，并使用一个变量来保存缓冲区的大小。
2.  根据通过以前的 [**WdfUsbTargetDeviceRetrieveConfigDescriptor**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdeviceretrieveconfigdescriptor) 调用接收的大小分配更大的缓冲区。
3.  再次调用 [**WdfUsbTargetDeviceRetrieveConfigDescriptor**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdeviceretrieveconfigdescriptor) ，并指定指向步骤2中分配的新缓冲区的指针。

```cpp
 NTSTATUS RetrieveDefaultConfigurationDescriptor (
    _In_  WDFUSBDEVICE  UsbDevice,
    _Out_ PUSB_CONFIGURATION_DESCRIPTOR *ConfigDescriptor 
    )
{
    NTSTATUS ntStatus = -1;

    USHORT sizeConfigDesc;

    PUSB_CONFIGURATION_DESCRIPTOR fullConfigDesc = NULL;

    PAGED_CODE();

    *ConfigDescriptor  = NULL;

    ntStatus = WdfUsbTargetDeviceRetrieveConfigDescriptor (
        UsbDevice, 
        NULL,
        &sizeConfigDesc);

    if (sizeConfigDesc == 0)
    {
        TraceEvents(TRACE_LEVEL_ERROR, TRACE_DEVICE, 
            "%!FUNC! Could not retrieve the configuration descriptor size.");

        goto Exit;
    }
    else
    {
        fullConfigDesc = (PUSB_CONFIGURATION_DESCRIPTOR) ExAllocatePoolWithTag (
            NonPagedPool, 
            sizeConfigDesc,
            USBCLIENT_TAG);

        if (!fullConfigDesc)
        {
            ntStatus = STATUS_INSUFFICIENT_RESOURCES;
            goto Exit;
        }  
    }

    RtlZeroMemory (fullConfigDesc, sizeConfigDesc);

    ntStatus = WdfUsbTargetDeviceRetrieveConfigDescriptor (
        UsbDevice, 
        fullConfigDesc,
        &sizeConfigDesc);

    if (!NT_SUCCESS(ntStatus))
    {           
        TraceEvents(TRACE_LEVEL_ERROR, TRACE_DEVICE, 
            "%!FUNC! Could not retrieve the configuration descriptor.");

        goto Exit;
    }

    *ConfigDescriptor = fullConfigDesc;

Exit:

    return ntStatus;   
}
```

**若要通过提交 URB 获取配置描述符，请执行以下步骤：**

1.  通过调用 [**WdfUsbTargetDeviceCreateUrb**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicecreateurb) 方法来分配 URB。
2.  通过调用 [**UsbBuildGetDescriptorRequest**](/previous-versions/ff538943(v=vs.85)) 宏来设置 URB 的格式。 URB 的传输缓冲区必须指向足够大的缓冲区，以容纳 [**USB \_ 配置 \_ 描述符**](/windows-hardware/drivers/ddi/usbspec/ns-usbspec-_usb_configuration_descriptor) 结构。
3.  通过调用 [**WdfRequestSend**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestsend) 或 [**WDFUSBTARGETDEVICESENDURBSYNCHRONOUSLY**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicesendurbsynchronously)，将 URB 提交为 WDF 请求对象。
4.  请求完成后，检查[**USB \_ 配置 \_ 描述符**](/windows-hardware/drivers/ddi/usbspec/ns-usbspec-_usb_configuration_descriptor)的**wTotalLength**成员。 该值指示包含完整配置描述符所需的缓冲区大小。
5.  根据在 **wTotalLength**中检索到的大小分配更大的缓冲区。
6.  用更大的缓冲区发出同一请求。

下面的示例代码演示了用于获取第 i 个配置的配置信息的请求的 [**UsbBuildGetDescriptorRequest**](/previous-versions/ff538943(v=vs.85)) 调用：

```cpp
NTSTATUS FX3_RetrieveConfigurationDescriptor (
    _In_ WDFUSBDEVICE  UsbDevice,
    _In_ PUCHAR ConfigurationIndex,
    _Out_ PUSB_CONFIGURATION_DESCRIPTOR *ConfigDescriptor 
    )
{
    NTSTATUS ntStatus = STATUS_SUCCESS;

    USB_CONFIGURATION_DESCRIPTOR configDesc;
    PUSB_CONFIGURATION_DESCRIPTOR fullConfigDesc = NULL;

    PURB urb = NULL;

    WDFMEMORY urbMemory = NULL;

    PAGED_CODE();

    RtlZeroMemory (&configDesc, sizeof(USB_CONFIGURATION_DESCRIPTOR));
    *ConfigDescriptor = NULL;

    // Allocate an URB for the get-descriptor request. 
    // WdfUsbTargetDeviceCreateUrb returns the address of the 
    // newly allocated URB and the WDFMemory object that 
    // contains the URB.

    ntStatus = WdfUsbTargetDeviceCreateUrb (
        UsbDevice,
        NULL,
        &urbMemory,
        &urb);

    if (!NT_SUCCESS (ntStatus))
    {
        TraceEvents(TRACE_LEVEL_ERROR, TRACE_DEVICE, 
            "%!FUNC! Could not allocate URB for an open-streams request.");

        goto Exit;
    }

       // Format the URB.
    UsbBuildGetDescriptorRequest (
        urb,                                                        // Points to the URB to be formatted
        (USHORT) sizeof( struct _URB_CONTROL_DESCRIPTOR_REQUEST ),  // Size of the URB.
        USB_CONFIGURATION_DESCRIPTOR_TYPE,                          // Type of descriptor
        *ConfigurationIndex,                                        // Index of the configuration
        0,                                                          // Not used for configuration descriptors
        &configDesc,                                                // Points to a USB_CONFIGURATION_DESCRIPTOR structure
        NULL,                                                       // Not required because we are providing a buffer not MDL
        sizeof(USB_CONFIGURATION_DESCRIPTOR),                       // Size of the USB_CONFIGURATION_DESCRIPTOR structure.
        NULL                                                        // Reserved.
        );

       // Send the request synchronously.
    ntStatus = WdfUsbTargetDeviceSendUrbSynchronously (
        UsbDevice,
        NULL,
        NULL,
        urb);

    if (configDesc.wTotalLength == 0)
    {
        TraceEvents(TRACE_LEVEL_ERROR, TRACE_DEVICE, 
            "%!FUNC! Could not retrieve the configuration descriptor size.");

        ntStatus = USBD_STATUS_INAVLID_CONFIGURATION_DESCRIPTOR;

        goto Exit;
    }

    // Allocate memory based on the retrieved size. 
       // The allocated memory is released by the caller.
    fullConfigDesc = (PUSB_CONFIGURATION_DESCRIPTOR) ExAllocatePoolWithTag (
        NonPagedPool, 
        configDesc.wTotalLength,
        USBCLIENT_TAG);

    RtlZeroMemory (fullConfigDesc, configDesc.wTotalLength);

    if (!fullConfigDesc)
    {
        ntStatus = STATUS_INSUFFICIENT_RESOURCES;

        goto Exit;
    }

       // Format the URB.
    UsbBuildGetDescriptorRequest (
        urb,                                                        
        (USHORT) sizeof( struct _URB_CONTROL_DESCRIPTOR_REQUEST ),  
        USB_CONFIGURATION_DESCRIPTOR_TYPE,                          
        *ConfigurationIndex,                                         
        0,                                                          
        fullConfigDesc,                                                 
        NULL,                                                       
        configDesc.wTotalLength,                       
        NULL                                                        
        );

       // Send the request again.
    ntStatus = WdfUsbTargetDeviceSendUrbSynchronously (
        UsbDevice,
        NULL,
        NULL,
        urb);

    if ((fullConfigDesc->wTotalLength == 0) || !NT_SUCCESS (ntStatus))
    {
        TraceEvents(TRACE_LEVEL_ERROR, TRACE_DEVICE, 
            "%!FUNC! Could not retrieve the configuration descriptor.");

        ntStatus = USBD_STATUS_INAVLID_CONFIGURATION_DESCRIPTOR;

        goto Exit;
    }

       // Return to the caller.
    *ConfigDescriptor = fullConfigDesc;

Exit:

    if (urbMemory)
    {
        WdfObjectDelete (urbMemory);
    }

    return ntStatus;   
}
```

当设备返回配置描述符时，请求缓冲区会用接口描述符填充所有备用设置，并使用特定备用设置中所有终结点的终结点说明符。 对于 [USB 设备布局](usb-device-layout.md)中描述的设备，下图说明了配置信息在内存中的布局方式。

![说明配置描述符布局的关系图](images/usbconfig.png)

[**USB \_ 接口 \_ 描述符**](/windows-hardware/drivers/ddi/usbspec/ns-usbspec-_usb_interface_descriptor)的从零开始的**bInterfaceNumber**成员在配置中区分接口。 对于给定的接口，从零开始的 **bAlternateSetting** 成员区分接口的备用设置。 设备按照 **bInterfaceNumber** 值顺序返回接口描述符，然后按照 **bAlternateSetting** 值的顺序返回。

若要在配置中搜索给定的接口描述符，客户端驱动程序可以调用 [**USBD \_ ParseConfigurationDescriptorEx**](/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_parseconfigurationdescriptorex)。 在调用中，客户端驱动程序在配置中提供开始位置。 或者，驱动程序可以指定接口号、替代设置、类、子类或协议。 例程返回指向下一个匹配接口描述符的指针。

若要检查终结点或字符串描述符的配置描述符，请使用 [**USBD \_ ParseDescriptors**](/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_parsedescriptors) 例程。 调用方提供配置中的起始位置和描述符类型，如 USB \_ 字符串 \_ 描述符 \_ 类型或 usb \_ 终结点 \_ 描述符 \_ 类型。 例程返回指向下一个匹配描述符的指针。

## <a name="related-topics"></a>相关主题
[如何为 USB 设备选择配置](how-to-select-a-configuration-for-a-usb-device.md)  
[USB 描述符](usb-descriptors.md)