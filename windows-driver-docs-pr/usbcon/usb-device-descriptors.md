---
Description: The device descriptor contains information about a USB device as a whole. This topic describes the USB_DEVICE_DESCRIPTOR structure and includes information about how a client driver can send a get-descriptor request to obtain the device descriptor.
title: USB 设备描述符
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9cc586d3575f648784d45b99544e029d0d3af7c8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56568509"
---
# <a name="usb-device-descriptors"></a>USB 设备描述符


设备描述符包含有关 USB 设备作为一个整体的信息。 本主题介绍[ **USB\_设备\_描述符**](https://msdn.microsoft.com/library/windows/hardware/ff539280)结构，并包含有关客户端驱动程序如何发送 get 描述符请求以获取设备信息描述符。

每个通用串行总线 (USB) 设备必须能够提供包含有关设备的相关信息的单个设备描述符。 [ **USB\_设备\_描述符**](https://msdn.microsoft.com/library/windows/hardware/ff539280)结构描述设备描述符。 Windows 使用该信息来派生不同组的信息。 例如， **idVendor**并**idProduct**字段分别指定供应商和产品标识符。 Windows 使用这些字段值来构造*硬件 ID*设备。 若要查看特定设备的硬件 ID，请打开**设备管理器**和查看设备属性。 在中**详细信息**选项卡上，**硬件 Id**属性值指示的硬件 ID ("USB\\*XXX*") 生成的 Windows。 **BcdUSB**字段指示设备是否符合的 USB 规范的版本。 例如，0x0200 指示该设备的设计根据 USB 2.0 规范。 **BcdDevice**值指示设备定义修订号。 使用 USB 驱动程序堆栈**bcdDevice**，连同**idVendor**并**idProduct**，以便生成硬件和设备兼容 Id。 您可以查看与中的标识符**设备管理器**。 设备描述符还指示设备支持的配置的总数。

当设备连接到主计算机在高速能力比全速容量中的连接时，设备可能会报告其设备描述符中的不同信息。 设备不得更改设备描述符中的连接，包括电源状态更改期间的生命周期内包含的信息。

获得通过控制传输的设备描述符。 在传输中的请求类型是获取描述符和接收方是设备。 客户端驱动程序可以启动该传输中通过两种方式： 使用框架 USB 目标设备对象或发送的请求信息 URB。

-   [获取设备描述符](#getting--the-device-descriptor)
-   [示例设备描述符](#sample-device-descriptor)

## <a name="getting-the-device-descriptor"></a>获取设备描述符


只有在创建框架 USB 目标设备对象后，Windows 驱动程序框架 (WDF) 客户端驱动程序可以获取设备描述符。

KMDF 驱动程序必须通过调用获取 USB 目标设备对象的 WDFUSBDEVICE 句柄[ **WdfUsbTargetDeviceCreate**](https://msdn.microsoft.com/library/windows/hardware/ff550077)。 通常，客户端驱动程序会调用**WdfUsbTargetDeviceCreate**中的驱动程序[ *EvtDevicePrepareHardware* ](https://msdn.microsoft.com/library/windows/hardware/ff540880)回调实现。 然后，客户端驱动程序必须调用[ **WdfUsbTargetDeviceGetDeviceDescriptor** ](https://msdn.microsoft.com/library/windows/hardware/ff550090)方法。 在调用完成后，在调用方分配中收到的设备描述符[ **USB\_设备\_描述符**](https://msdn.microsoft.com/library/windows/hardware/ff539280)结构。

UMDF 驱动程序必须 framework 设备对象中查询[ **IWDFUsbTargetDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff560362)指针，然后调用[ **IWDFUsbTargetDevice::RetrieveDescriptor**](https://msdn.microsoft.com/library/windows/hardware/ff560362_retrievedescriptor)方法并指定 USB\_设备\_描述符\_与描述符类型的类型。

主机还可以通过发送 URB 获取设备描述符。 此方法仅适用于内核模式驱动程序。 但是，客户端驱动程序应永远不会需要将发送此类请求 URB，除非该驱动程序基于 Windows 驱动程序模型 (WDM)。 此类驱动程序必须分配[ **URB** ](https://msdn.microsoft.com/library/windows/hardware/ff538923)结构，然后调用[ **UsbBuildGetDescriptorRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff538943)宏，以指定格式请求 URB。 驱动程序然后可以通过将提交到 USB 驱动程序堆栈 URB 发送请求。 有关详细信息，请参阅[如何提交 URB](send-requests-to-the-usb-driver-stack.md)。

此代码示例显示了格式由与相应 URB pURB 指向的缓冲区的 UsbBuildGetDescriptorRequest 调用：

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


此示例显示了 USB 网络摄像机设备的设备描述符 (请参阅[USB 设备布局](usb-device-layout.md))，获得使用 USBView 应用程序：

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

在上述示例中，将看到，设备已开发了根据 USB 规范，版本 2.0。 请注意**bDeviceClass**， **bDeviceSubClass**，并**bDeviceProtocol**值。 这些值指示该设备包含一个或多个 USB 接口关联描述符的可用于分组每个函数的多个接口。 有关详细信息，请参阅[USB 接口关联描述符](usb-interface-association-descriptor.md)。

接下来，请参阅的值**bMaxPacketSize0**。 此值指示的默认终结点的最大数据包大小。 此示例设备可以传输最多 64 个字节的数据通过其默认终结点。

通常情况下，若要配置设备，客户端驱动程序获取有关所支持的配置信息的设备中获取设备描述符后。 若要确定设备支持的配置的数量，请检查**bNumConfigurations**返回的结构的成员。 此设备支持的一种配置。 若要获取有关 USB 配置的信息，该驱动程序必须获取[USB 配置描述符](usb-configuration-descriptors.md)。

## <a name="related-topics"></a>相关主题
[USB 描述符](usb-descriptors.md)  
[USB 配置描述符](usb-configuration-descriptors.md)  



