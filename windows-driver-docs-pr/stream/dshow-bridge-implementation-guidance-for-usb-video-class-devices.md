---
title: 适用于 UVC 设备的 DShow 桥实现指南
description: 提供了适用于 UVC 设备 DShow 桥实现指南。
ms.date: 05/17/2018
ms.localizationpriority: medium
ms.openlocfilehash: 8ccaa5be9ac2ff404335aaa5dc2f3a31caf75464
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63363612"
---
# <a name="dshow-bridge-implementation-guidance-for-uvc-devices"></a>适用于 UVC 设备的 DShow 桥实现指南

本主题提供了用于 DShow 桥配置的照相机和设备的符合 USB 视频类 (UVC) 规范实现指南。 该平台使用[Microsoft OS 描述符](https://docs.microsoft.com/windows-hardware/drivers/usbcon/microsoft-defined-usb-descriptors)从 USB 总线标准配置 DShow 桥。 扩展属性 OS 描述符是 USB 标准描述符的扩展，USB 设备使用它来返回尚未通过标准规范启用的 Windows 特定设备属性。

## <a name="overview"></a>概述

Microsoft 相机捕获堆栈包括名为 DirectShow 和现代框架调用多媒体 Foundation 的旧版 framework 堆栈。 Ihv 和 Oem 不得不编写为其设备以满足这两个管道组件。

使用桥接 DShow 管道与媒体基础平台的意向编写 DShow 桥。 这样，则返回 true 的通用驱动程序，因此 Ihv 和 Oem 可以编写可以使用 MediaFoundation 和 DShow 运行应用程序 Windows 版本 1607年及更高版本的驱动程序。 使用 DShow 桥参加启用，DShow 应用程序和共享应用程序可以共享相同的照相机硬件并发。

Ihv 和 Oem 可能需要免除策略来管理 DShow 管道。 合作伙伴可以支持使用操作系统描述符的以下功能：

-   **加入或退出 DShow 桥**:设备可以选择加入或退出到管道桥更好地适合其需求。 现代的管道更完整地记录，并利用在多个版本中添加到操作系统的功能。 旧的管道，处于维护模式下，滞后。

-   **帧 server 中的 MJPEG 解压缩**:帧服务器是虚拟化照相机设备的服务。 这样，从设备插针，以在多个客户端之间共享。 无优化的 Media Foundation 解压缩程序的体系结构可以使用此功能进行解码帧 Server 中的 MJPEG。 未压缩时，转换媒体 formats(YUY2) 提供给多个应用程序。 流的多个可能的客户端的解压缩仅一次。 这提高了应用程序的性能。 下图显示了相机捕获管道：

![相机捕获管道](images/camera-capture-pipeline.png)

Oem 和 Ihv 打包其 USB 摄像机设备可以使用 USB 总线标准的扩展属性操作系统功能描述符规范不需求助于其 UVC 驱动程序的任何 INF 文件更改的情况下配置 DShow 桥。

OS 描述符允许设备可以定义的 USB 设备注册表属性或复合设备。

若要配置 DShow 桥使用 USB 操作系统描述符，主机软件应创建每个 USB 设备接口的以下注册表项：

> HKLM\\SYSTEM\\CurrentControlSet\\Enum\\USB\\&lt;*DeviceVID&PID*&gt;\\&lt;*DeviceInstance*&gt;\\Device Parameters
>
> DWORD:**EnableDshowRedirection**

**EnableDshowRedirection**注册表值是位掩码值用于配置 DShow 桥，如下面的表中所述。

| 位掩码 | 描述 | 备注 |
|---|---|---|
| 0x00000001 | 选择加入 DShow 桥 | 0 – 选择退出<br>1 – 选择加入的  |
| 0x00000002 | 启用 MJPEG 解码帧服务器中 （请参阅下面的备注） | 0-MJPEG 压缩媒体类型公开 （无操作）<br>1 – 公开从 MJPEG (YUY2) 的已翻译的未压缩的媒体类型 |

> [!NOTE]
> 使 MJPEG 解码一次且仅未压缩的媒体类型提供对应用程序。

## <a name="example-layouts"></a>示例布局

针对以下规范包含如下示例：

-   Microsoft 操作系统描述符规范 1.0 扩展

-   Microsoft OS 2.0 描述符规范

### <a name="microsoft-os-extended-property-descriptors-specification-version-10"></a>Microsoft 操作系统的扩展属性描述符规范版本 1.0

扩展的属性操作系统描述符有两个组件

-   固定长度标头部分

-   一个或多个可变长度自定义属性部分中，该过程的标头部分

#### <a name="header-section"></a>标头部分

标头部分将介绍整个扩展的属性描述符，包括总长度和版本号。

| 偏移量 | 字段      | 大小 （字节） | ReplTest1      | Description                     |
|--------|------------|--------------|------------|---------------------------------|
| 0      | dwLength   | 4            | 0x0000004c | 十进制 76                      |
| 4      | bcdVersion | 2            | 0x0100     | 版本 1.0                     |
| 6      | wIndex     | 2            | 0x005      | 扩展的属性 OS 描述符 |
| 8      | wCount     | 2            | 0x0001     | 一个自定义属性             |

#### <a name="custom-property-section"></a>自定义属性部分

USB HID 设备的扩展的属性的操作系统描述符都有一个自定义属性部分中创建**EnableDshowRedirection** DWORD 注册表项。

| 偏移量 | 字段 | 大小 （字节） | ReplTest1 |
|--------|----------------------|---------|-------------------------------------------|
| 0      | dwSize               | 4       | 0x00000042 （此属性 66 字节为单位）   |
| 4      | dwPropertyDataType   | 4       | 0x00000004 (REG\_DWORD\_LITTLE\_ENDIAN)   |
| 8      | wPropertyNameLength  | 2       | 0x0030                                    |
| 10     | bPropertyName        | 48      | **EnableDshowRedirection** （Unicode 字符串） |
| 58     | dwPropertyDataLength | 4       | 0x00000004 (Sizeof(DWORD))                |
| 62     | bPropertyData        | 4       | 0x00000001 （DWORD 数据）                   |

### <a name="microsoft-os-20-descriptors-specification"></a>Microsoft OS 2.0 描述符规范

此示例演示如何使用 Microsoft 2.0 描述符集以提供一个单一的 DWORD 注册表值**EnableDshowRedirection** ，适用于 Windows 版本。

#### <a name="custom-property-section"></a>自定义属性部分

| 偏移量 | 字段 | 大小 （字节） | ReplTest1 |
|--------|----------------------|----------|-----------------------------------------|
| 0      | wLength              | 2        | 此描述符的长度 （字节）      |
| 4      | wDescriptorType      | 2        | 0x00000004 (REG\_DWORD\_LITTLE\_ENDIAN) |
| 8      | wPropertyDataType    | 2        | 0x0030                                  |
|        | wPropertyNameLength  | 2        |                                         |
| 10     | PropertyName         | 变量 | 属性名称的长度             |
| 58     | dwPropertyDataLength | 2        | 属性数据的长度                 |
| 62     | PropertyData         | 变量 | 属性数据                           |


```cpp
UCHAR Example2\_MSOS20DescriptorSetForFutureWindows\[0x48\] =
{
    //
    // Microsoft OS 2.0 Descriptor Set Header
    //
    0x0A, 0x00,                 // wLength - 12 bytes
    0x00, 0x00,                 // MSOS20_SET_HEADER_DESCRIPTOR
    0x00, 0x00, 0x0?, 0x06,     // dwWindowsVersion – 0x06030000 for future Windows version
    0x4A, 0x00,                 // wTotalLength – 72 bytes

    //
    // Microsoft OS 2.0 Registry Value Feature Descriptor
    //
    0x3E, 0x00,                 // wLength - 62 bytes
    0x04, 0x00,                 // wDescriptorType – 5 for Registry Property
    0x04, 0x00,                 // wPropertyDataType - 4 for REG_DWORD
    0x30, 0x00,                 // wPropertyNameLength – 48 bytes
    0x45, 0x00, 0x6E, 0x00,     // Property Name - "EnableDshowRedirection"
    0x61, 0x00, 0x62, 0x00,
    0x6C, 0x00, 0x65, 0x00,
    0x44, 0x00, 0x73, 0x00,
    0x68, 0x00, 0x6F, 0x00,
    0x77, 0x00, 0x52, 0x00,
    0x65, 0x00, 0x64, 0x00,
    0x69, 0x00, 0x72, 0x00,
    0x65, 0x00, 0x63, 0x00,
    0x74, 0x00, 0x69, 0x00,
    0x6F, 0x00, 0x6E, 0x00,
    0x00, 0x00, 0x00, 0x00,
    0x04, 0x00,                 // wPropertyDataLength – 4 bytes
    0x00, 0x00, 0x00, 0x00      // PropertyData – 0x00000003 (see note below)
}
```

> [!NOTE]
> 0x00000003:-启用 DShow 桥和 MJPEG 解码 FrameServer，例如，在源中

### <a name="resources"></a>资源

[Microsoft 操作系统描述符的 USB 设备](https://docs.microsoft.com/windows-hardware/drivers/usbcon/microsoft-defined-usb-descriptors)

[USB 泛型父驱动程序 (Usbccgp.sys)](https://docs.microsoft.com/windows-hardware/drivers/usbcon/usb-common-class-generic-parent-driver)

[USB 规范](http://www.usb.org/developers/docs)
