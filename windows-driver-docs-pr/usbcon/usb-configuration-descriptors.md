---
Description: USB 设备公开的接口称为 USB 配置一系列的窗体中的其功能。
title: USB 配置描述符
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b445f88f648983cdcc20bba5f52cd317d8806c8c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331654"
---
# <a name="usb-configuration-descriptors"></a>USB 配置描述符


USB 设备公开的接口称为 USB 配置一系列的窗体中的其功能。 每个接口由一个或多个备用的设置，和每个备用设置由一组终结点组成。 本主题介绍与 USB 配置相关联的各种描述符。

配置描述符中介绍了 USB 配置 (请参阅[ **USB\_配置\_描述符**](https://msdn.microsoft.com/library/windows/hardware/ff539241)结构)。 配置描述符包含有关配置和其接口，替代设置和其终结点的信息。 中所述的每个接口描述符或替代设置[ **USB\_界面\_描述符**](https://msdn.microsoft.com/library/windows/hardware/ff540065)结构。 在配置中，每个接口描述符后跟在内存中所有的终结点描述符的接口和替代设置。 每个终结点描述符存储在[ **USB\_终结点\_描述符**](https://msdn.microsoft.com/library/windows/hardware/ff539317)结构。

例如，考虑 USB 网络摄像机设备中所述[USB 设备布局](usb-device-layout.md)。 设备支持使用两个接口的配置和 （索引 0） 的第一个接口支持两个替代设置。

下面的示例显示了 USB 网络摄像机设备的配置描述符：

``` syntax
Configuration Descriptor:
wTotalLength:         0x02CA
bNumInterfaces:       0x02
bConfigurationValue:  0x01
iConfiguration:       0x00
bmAttributes:         0x80 (Bus Powered )
MaxPower:             0xFA (500 mA)
```

**BConfigurationValue**字段指示设备的固件中定义的配置的编号。 客户端驱动程序使用该数字值来选择活动的配置。 有关详细信息[USB 设备配置](configuring-usb-devices.md)，请参阅[如何选择一种配置 USB 设备](how-to-select-a-configuration-for-a-usb-device.md)。 USB 配置还指示某些 power 特征。 **BmAttributes**包含一个位掩码，指示配置是否支持远程唤醒功能，以及设备是总线供电还是自供电。 **MaxPower**字段指定打开设备时是总线的设备可以从主机中，绘制的最大功率 （以 milliamp 为单位）。 配置描述符还指示接口的总数 (**bNumInterfaces**) 的设备支持。

下面的示例演示为备用设置 0 的网络摄像机设备接口 0 接口描述符：

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

在前面的示例，请注意**bInterfaceNumber**并**bAlternateSetting**字段值。 这些字段包含客户端驱动程序将使用激活的接口和一个其替代设置的索引值。 用于激活、 驱动程序将选择接口请求发送到 USB 驱动程序堆栈。 然后，驱动程序堆栈生成的标准控件请求 （设置接口），并将其发送到设备。 请注意**bInterfaceClass**字段。 接口描述符或任何其替代设置描述符指定的类代码、 子类和协议。 0x0E 的值指示该接口是视频设备类。 另请注意**iInterface**字段。 该值指示两个字符串描述符附加到接口描述符。 字符串描述符包含 Unicode 在设备枚举过程中用于标识功能的说明。 有关字符串描述符的详细信息，请参阅[USB 字符串描述符](usb-string-descriptors.md)。

每个终结点，接口中的描述的输入或输出设备的单个流。 为不同类型的函数支持流的设备有多个接口。 支持适用于函数的几个流的设备可以在单个接口上支持多个终结点。

所有类型的终结点 （除默认终结点） 必须都提供终结点描述符，以便主机可以获取有关终结点的信息。 终结点描述符包括信息，例如其地址、 类型、 方向，并可以处理终结点的数据量。 将数据传输至终结点基于该信息。

下面的示例显示了网络摄像头设备的终结点描述符：

``` syntax
Endpoint Descriptor:
bEndpointAddress:   0x82  IN
bmAttributes:       0x01
wMaxPacketSize:     0x0080 (128)
bInterval:          0x01
```

**BEndpointAddress**字段指定包含终结点号 (位 3..0) 和终结点 (位 7) 的方向的唯一的终结点地址。 通过阅读这些值在前面的示例，我们可以确定描述符描述其终结点号为 2 的在终结点。 **BmAttributes**属性指示终结点类型为等时。 **WMaxPacketSizefield**指示最大字节数的终结点可以发送或接收在单个事务中。 位 12..11 指示可以每 microframe 发送的事务总数。 **BInterval**指示终结点发送或接收数据的频率。

## <a name="how-to-get-the-configuration-descriptor"></a>如何获取配置描述符


从设备通过标准的设备请求获取配置描述符 (获取\_描述符)，这作为控制传输发送的 USB 驱动程序堆栈。 USB 客户端驱动程序可以通过以下方式之一启动请求：

- 如果设备支持只有一个配置，最简单方法是调用框架提供[ **WdfUsbTargetDeviceRetrieveConfigDescriptor** ](https://msdn.microsoft.com/library/windows/hardware/ff550098)方法。
- 对于支持多个配置设备，如果客户端驱动程序想要获取的描述符以外的第一个，该驱动程序的配置必须提交 URB。 若要提交 URB，驱动程序必须分配、 设置格式，并提交到 USB 驱动程序堆栈 URB。

  若要分配 URB，客户端驱动程序必须调用[ **WdfUsbTargetDeviceCreateUrb** ](https://msdn.microsoft.com/library/windows/hardware/hh439423)方法。 该方法接收指向分配的 USB 驱动程序堆栈 URB 的指针。

  若要设置格式 URB，客户端驱动程序可以使用[ **UsbBuildGetDescriptorRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff538943)宏。 宏 URB，例如设备定义的配置数量为其检索描述符中设置所有所需的信息。 URB 函数设置为 URB\_函数\_获取\_描述符\_FROM\_设备 (请参阅[  **\_URB\_控件\_描述符\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff540357)) 和描述符的类型设置为 USB\_配置\_描述符\_类型。 通过使用 URB 中包含的信息，USB 驱动程序堆栈生成的标准控件请求，并将其发送到设备。

  若要提交 URB，客户端驱动程序必须使用 WDF 请求对象。 若要以异步方式发送到 USB 驱动程序堆栈的请求对象，该驱动程序必须调用[ **WdfRequestSend**](https://msdn.microsoft.com/library/windows/hardware/ff550027)方法。 若要以同步方式发送，调用[ **WdfUsbTargetDeviceSendUrbSynchronously** ](https://msdn.microsoft.com/library/windows/hardware/ff550105)方法。

  <strong>WDM 驱动程序: * * Windows 驱动程序模型 (WDM) 客户端驱动程序只能获取通过提交 URB 配置描述符。若要分配 URB，驱动程序必须调用[ </strong>USBD\_UrbAllocate<strong> ](<https://msdn.microsoft.com/library/windows/hardware/hh406250>)例程。若要设置格式 URB，驱动程序必须调用[ </strong>UsbBuildGetDescriptorRequest * *](<https://msdn.microsoft.com/library/windows/hardware/ff538943>)宏。 若要提交 URB，驱动程序必须将 URB IRP，与相关联并提交到 USB 驱动程序堆栈 IRP。 有关详细信息，请参阅[如何提交 URB](send-requests-to-the-usb-driver-stack.md)。

在 USB 配置中，接口和其替代设置的数量是可变的。 因此，很难预测保存配置描述符所需的缓冲区的大小。 客户端驱动程序必须收集两个步骤中的所有该信息。 首先，确定哪个大小保留所有配置描述符，然后发出一个请求以检索整个描述符所需的缓冲区。 客户端驱动程序可以通过以下方式之一获取大小：

**若要获取通过调用 WdfUsbTargetDeviceRetrieveConfigDescriptor 配置描述符，执行以下步骤：**

1.  获取通过调用保存的所有配置信息所都需的缓冲区的大小[ **WdfUsbTargetDeviceRetrieveConfigDescriptor**](https://msdn.microsoft.com/library/windows/hardware/ff550098)。 该驱动程序必须传递 NULL 缓冲区和一个变量来保存缓冲区的大小。
2.  分配基于上一收到的大小较大的缓冲区[ **WdfUsbTargetDeviceRetrieveConfigDescriptor** ](https://msdn.microsoft.com/library/windows/hardware/ff550098)调用。
3.  调用[ **WdfUsbTargetDeviceRetrieveConfigDescriptor** ](https://msdn.microsoft.com/library/windows/hardware/ff550098)再次并指定指向分配在步骤 2 中的新缓冲区的指针。

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

**若要通过提交 URB 获取配置描述符，执行以下步骤：**

1.  通过调用分配 URB [ **WdfUsbTargetDeviceCreateUrb** ](https://msdn.microsoft.com/library/windows/hardware/hh439423)方法。
2.  通过调用格式化 URB [ **UsbBuildGetDescriptorRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff538943)宏。 URB 的传输缓冲区必须指向缓冲区足以容纳[ **USB\_配置\_描述符**](https://msdn.microsoft.com/library/windows/hardware/ff539241)结构。
3.  通过调用 WDF request 对象作为提交 URB [ **WdfRequestSend** ](https://msdn.microsoft.com/library/windows/hardware/ff550027)或[ **WdfUsbTargetDeviceSendUrbSynchronously**](https://msdn.microsoft.com/library/windows/hardware/ff550105)。
4.  在请求完成后，检查**wTotalLength**的成员[ **USB\_配置\_描述符**](https://msdn.microsoft.com/library/windows/hardware/ff539241)。 该值指示包含完整的配置描述符所需的缓冲区的大小。
5.  分配基于中检索到的大小较大的缓冲区**wTotalLength**。
6.  使用更大的缓冲区中发出相同的请求。

以下示例代码所示[ **UsbBuildGetDescriptorRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff538943)调用请求获取的第 i 个配置的配置信息：

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

当设备返回配置描述符时，会为请求缓冲区填充接口描述符的所有替代设置和特定的替代设置中的所有终结点的终结点描述符。 为设备中所述[USB 设备布局](usb-device-layout.md)下, 图说明了配置信息在内存中的布局方式。

![说明配置描述符布局的关系图](images/usbconfig.png)

从零开始**bInterfaceNumber**的成员[ **USB\_接口\_描述符**](https://msdn.microsoft.com/library/windows/hardware/ff540065)区分配置内的接口。 对于给定的接口，从零开始**bAlternateSetting**成员区分接口的替代设置。 设备中的顺序返回接口描述符**bInterfaceNumber**值，然后按顺序**bAlternateSetting**值。

若要搜索的配置中的给定的接口描述符，客户端驱动程序可以调用[ **USBD\_ParseConfigurationDescriptorEx**](https://msdn.microsoft.com/library/windows/hardware/ff539102)。 在调用中，客户端驱动程序提供配置内的起始位置。 或者，驱动程序可以指定接口号、 替代设置、 类、 一个子类或一种协议。 例程将返回一个指针，到下一个匹配的接口描述符。

若要检查终结点或字符串描述符的配置描述符，使用[ **USBD\_ParseDescriptors** ](https://msdn.microsoft.com/library/windows/hardware/ff539109)例程。 调用方提供配置和描述符类型，如 USB 内的起始位置\_字符串\_描述符\_类型或 USB\_终结点\_描述符\_类型。 例程将返回一个指针，到下一个匹配的描述符。

## <a name="related-topics"></a>相关主题
[如何选择一种配置 USB 设备](how-to-select-a-configuration-for-a-usb-device.md)  
[USB 描述符](usb-descriptors.md)  



