---
Description: 设备描述符同时包含有关 USB 设备的信息。 本主题介绍 USB_DEVICE_DESCRIPTOR 结构，并包括有关客户端驱动程序如何发送获取描述符请求以获取设备描述符的信息。
title: USB 设备描述符
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a7f6a01644f1b7890d3956d1623a6d70a320131b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844828"
---
# <a name="usb-device-descriptors"></a>USB 设备描述符


设备描述符同时包含有关 USB 设备的信息。 本主题介绍[**USB\_设备\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbspec/ns-usbspec-_usb_device_descriptor)结构，并包括有关客户端驱动程序如何发送获取描述符请求以获取设备描述符的信息。

每个通用串行总线（USB）设备必须能够提供单个设备描述符，其中包含有关设备的相关信息。 [**USB\_设备\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbspec/ns-usbspec-_usb_device_descriptor)结构描述了设备描述符。 Windows 使用该信息来派生各种信息集。 例如，" **idVendor** " 和 " **idProduct** " 字段分别指定供应商和产品标识符。 Windows 使用这些字段值来构造设备的*硬件 ID* 。 若要查看特定设备的硬件 ID，请打开**设备管理器**并查看设备属性。 在 "**详细信息**" 选项卡中，"**硬件 id** " 属性值表示 WINDOWS 生成的硬件 id （"USB\\*XXX*"）。 **BcdUSB**字段指示设备符合的 USB 规范的版本。 例如，0x0200 指示设备按照 USB 2.0 规范设计。 **BcdDevice**值指示设备定义的修订号。 USB 驱动程序堆栈使用**bcdDevice**以及**idVendor**和**idProduct**来生成设备的硬件和兼容 id。 可以在**设备管理器**中查看这些标识符。 设备描述符还表明设备支持的配置总数。

当设备连接到主计算机的速度比全速容量大时，设备可能会在其设备描述符中报告不同的信息。 在连接的生存期内（包括电源状态更改期间），设备不得更改设备描述符中包含的信息。

宿主通过控件传输获取设备描述符。 在传输中，请求类型为 GET 描述符，接收方是设备。 客户端驱动程序可以通过以下两种方式之一来启动该传输：通过使用 framework USB 目标设备对象或发送包含请求信息的 URB。

-   [获取设备描述符](#getting-the-device-descriptor)
-   [示例设备描述符](#sample-device-descriptor)

## <a name="getting-the-device-descriptor"></a>获取设备描述符


Windows 驱动程序框架（WDF）客户端驱动程序只能在创建框架 USB 目标设备对象之后获取设备描述符。

KMDF 驱动程序必须通过调用[**WdfUsbTargetDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicecreate)获取 USB 目标设备对象的 WDFUSBDEVICE 句柄。 通常，客户端驱动程序会在驱动程序的[*EvtDevicePrepareHardware*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)回调实现中调用**WdfUsbTargetDeviceCreate** 。 之后，客户端驱动程序必须调用[**WdfUsbTargetDeviceGetDeviceDescriptor**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicegetdevicedescriptor)方法。 调用完成后，会在调用方分配的[**USB\_设备\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbspec/ns-usbspec-_usb_device_descriptor)结构中接收设备描述符。

UMDF 驱动程序必须在框架设备对象中查询[**IWDFUsbTargetDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nn-wudfusb-iwdfusbtargetdevice)指针，然后调用[**IWDFUsbTargetDevice：： RetrieveDescriptor**](https://msdn.microsoft.com/library/windows/hardware/ff560362_retrievedescriptor)方法并指定 USB\_设备\_描述符\_类型为描述符类型。

主机还可以通过发送 URB 来获取设备描述符。 此方法仅适用于内核模式驱动程序。 但是，客户端驱动程序绝不应发送此类请求的 URB，除非该驱动程序基于 Windows 驱动模型（WDM）。 此类驱动程序必须分配[**URB**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb)结构，然后调用[**UsbBuildGetDescriptorRequest**](https://docs.microsoft.com/previous-versions/ff538943(v=vs.85))宏来指定请求的 URB 格式。 然后，该驱动程序可以通过将 URB 提交到 USB 驱动程序堆栈来发送请求。 有关详细信息，请参阅[如何提交 URB](send-requests-to-the-usb-driver-stack.md)。

此代码示例演示了一个 UsbBuildGetDescriptorRequest 调用，该调用使用适当的 URB 格式化 pURB 指向的缓冲区：

```cpp
UsbBuildGetDescriptorRequest(
    pURB,                                                 // Points to the URB to be formatted
    sizeof(struct _URB_CONTROL_DESCRIPTOR_REQUEST),
    USB_DEVICE_DESCRIPTOR_TYPE,
    0,                                                    // Not used for device descriptors
    0,                                                    // Not used for device descriptors
    pDescriptor,                                          // Points to a USB_DEVICE_DESCRIPTOR structure
    NULL,
    sizeof(USB_DEVICE_DESCRIPTOR),
    NULL
);
```

## <a name="sample-device-descriptor"></a>示例设备描述符


此示例显示了通过使用 USBView 应用程序获得的 USB 网络摄像机设备（请参阅[Usb 设备布局](usb-device-layout.md)）的设备描述符：

``` syntax
Device Descriptor:
bcdUSB:             0x0200
bDeviceClass:         0xEF
bDeviceSubClass:      0x02
bDeviceProtocol:      0x01
bMaxPacketSize0:      0x40 (64)
idVendor:           0x045E (Microsoft Corporation)
idProduct:          0x0728
bcdDevice:          0x0100
iManufacturer:        0x01
0x0409: "Microsoft"
iProduct:             0x02
0x0409: "Microsoft LifeCam VX-5000"
0x0409: "Microsoft LifeCam VX-5000"
iSerialNumber:        0x00
bNumConfigurations:   0x01
```

在前面的示例中，你将看到设备按照每个 USB 规范（版本2.0）进行开发。 请注意**bDeviceClass**、 **bDeviceSubClass**和**bDeviceProtocol**值。 这些值表明设备包含一个或多个 USB 接口关联描述符，可用于对每个函数的多个接口进行分组。 有关详细信息，请参阅[USB 接口关联描述符](usb-interface-association-descriptor.md)。

接下来，请参阅**bMaxPacketSize0**的值。 此值指示默认终结点的最大数据包大小。 此示例设备可以通过其默认终结点最多传输64个字节的数据。

通常，若要配置设备，客户端驱动程序会在获取设备描述符后获取有关设备中支持的配置的信息。 若要确定设备支持的配置数，请检查返回的结构的**bNumConfigurations**成员。 此设备支持一个配置。 若要获取有关 USB 配置的信息，驱动程序必须获取[Usb 配置描述符](usb-configuration-descriptors.md)。

## <a name="related-topics"></a>相关主题
[USB 描述符](usb-descriptors.md)  
[USB 配置描述符](usb-configuration-descriptors.md)  



