---
title: 适用于 UVC 设备的 DShow 桥实现指南
description: 提供 UVC 设备的 DShow Bridge 实现指南。
ms.date: 12/16/2020
ms.localizationpriority: medium
ms.openlocfilehash: f33ede6bf48bcbf354b2cf0027a6c453168cc126
ms.sourcegitcommit: b14becba4beb4e7c843908710352ad60999f0c38
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/17/2020
ms.locfileid: "97612736"
---
# <a name="dshow-bridge-implementation-guidance-for-uvc-devices"></a>适用于 UVC 设备的 DShow 桥实现指南

本主题提供了为 DShow 桥配置照相机和设备的实现指南，这些设备符合 USB 视频类 (UVC) 规范。 该平台使用 USB 总线标准版中的 [MICROSOFT OS 描述符](../usbcon/microsoft-defined-usb-descriptors.md) 来配置 DShow 桥。 扩展属性 OS 描述符是 USB 标准描述符的扩展，USB 设备使用它来返回尚未通过标准规范启用的 Windows 特定设备属性。

## <a name="overview"></a>概述

Microsoft 相机捕获堆栈包含名为 DirectShow 的传统框架堆栈和称为多媒体基础的新式框架。 Ihv 和 Oem 必须为其设备编写组件来满足这两个管道的需要。

DShow 桥是通过将 DShow 管道与媒体基础平台桥接而编写的。 这可以实现真正的通用驱动程序，因此 Ihv 和 Oem 可以编写能够在 Windows 版本1607和更高版本上与 MediaFoundation 和 DShow 应用程序一起运行的驱动程序。 启用 DShow 桥选择启用后，DShow 应用程序和共享应用程序可以同时共享同一相机硬件。

Ihv 和 Oem 可能需要用于管理 DShow 管道的策略的例外。 合作伙伴可以使用 OS 描述符启用以下功能：

- 选择加入 **或退出 DShow 桥**：设备可以选择加入或离开桥，使管道更适合于其需求。 新式管道的记录更为全面，并利用多个版本中添加到操作系统的功能。 旧式管道处于维护模式，滞后一些。

- **FrameServer 中的 MJPEG 解压缩**： FrameServer 是一种用于虚拟化照相机设备的服务。 这允许在多个客户端之间共享设备的 Pin。 具有优化媒体基础解压缩程序的体系结构可以使用此功能在 FrameServer 中对 MJPEG 进行解码。 为多个应用程序提供了未压缩的已转换媒体格式 (YUY2) 。 流只是为多个可能的客户端解压缩一次。 这可以提高应用程序的性能。 下图显示了相机捕获管道：

![相机捕获管道](images/camera-capture-pipeline.png)

打包其 USB 照相机设备的 Oem 和 Ihv 可以使用 USB bus 标准的扩展属性 OS 功能描述符规范来配置 DShow 桥，而不会对其 UVC 驱动程序的任何 INF 文件进行更改。

操作系统描述符允许设备定义 USB 设备或复合设备的注册表属性。

若要使用 USB OS 描述符配置 DShow 桥，主机软件应为每个 USB 设备接口创建以下注册表项：

> HKLM \\ 系统 \\ CurrentControlSet \\ 枚举 \\ USB \\ &lt; *DeviceVID&PID* &gt; \\ &lt; *DeviceInstance* &gt; \\ 设备参数
>
> DWORD： **EnableDshowRedirection**

**EnableDshowRedirection** 注册表值是一个位掩码值，可用于配置 DShow 桥，如下表所述。

| 位掩码 | 说明 | 备注 |
|---|---|---|
| 0x00000001 | 选择加入 DShow Bridge | 0–选择退出<br>1–选择加入  |
| 0x00000002 | 在 FrameServer 中启用一次 MJPEG 解码 (参阅下面的注释)  | 0– MJPEG)  (<br>1-从 MJPEG 中公开翻译后的未压缩媒体类型 (YUY2)  |

> [!NOTE]
> 在 FrameServer 中启用一次 MJPEG 解码，然后在多个应用程序 (YUY2) 提供未压缩的已转换媒体格式。 流只是为多个可能的客户端解压缩一次。 这可以提高应用程序的性能。

## <a name="example-layouts"></a>示例布局

下面的示例包含以下规范：

- Microsoft OS 扩展描述符规范1。0

- Microsoft 操作系统2.0 描述符规范

### <a name="microsoft-os-extended-property-descriptors-specification-version-10"></a>Microsoft OS 扩展属性描述符规范版本1。0

扩展属性 OS 描述符包含两个组件

- 固定长度标头部分

- 标头部分后面的一个或多个可变长度自定义属性部分

#### <a name="header-section"></a>标题部分

标头部分描述了整个扩展属性说明符，其中包括总长度和版本号。

| Offset | 字段      | 大小（字节） | 值      | 说明                     |
|--------|------------|--------------|------------|---------------------------------|
| 0      | dwLength   | 4            | 0x0000004c | 76 decimal                      |
| 4      | bcdVersion | 2            | 0x0100     | 版本 1.0                     |
| 6      | wIndex     | 2            | 0x005      | 扩展属性 OS 描述符 |
| 8      | wCount     | 2            | 0x0001     | 一个自定义属性             |

#### <a name="custom-property-section-10-descriptor"></a>自定义属性部分 (1.0 描述符) 

USB HID 设备的扩展属性 OS 描述符包含一个用于创建 **EnableDshowRedirection** DWORD 注册表项的自定义属性部分。

| Offset | 字段 | 大小（字节） | 值 |
|--------|----------------------|---------|-------------------------------------------|
| 0      | dwSize               | 4       | 此属性的 0x00000042 (66 字节)    |
| 4      | dwPropertyDataType   | 4       | 0x00000004 (REG \_ DWORD \_ 小 \_ ENDIAN)    |
| 8      | wPropertyNameLength  | 2       | 0x0030                                    |
| 10     | bPropertyName        | 48      | **EnableDshowRedirection** (Unicode string)  |
| 58     | dwPropertyDataLength | 4       | 0x00000004 (Sizeof (DWORD) # A3                |
| 62     | bPropertyData        | 4       | 0x00000001 (DWORD 数据)                    |

### <a name="microsoft-os-20-descriptors-specification"></a>Microsoft 操作系统2.0 描述符规范

此示例演示如何使用 Microsoft 2.0 描述符集来提供适用于 Windows 版本的 **EnableDshowRedirection** 的单个 DWORD 注册表值。

#### <a name="custom-property-section-20-descriptor"></a>自定义属性部分 (2.0 描述符) 

| Offset | 字段 | 大小（字节） | 值 |
|--------|----------------------|----------|-----------------------------------------|
| 0      | wLength              | 2        | 此描述符的长度（以字节为单位）      |
| 4      | wDescriptorType      | 2        | 0x00000004 (REG \_ DWORD \_ 小 \_ ENDIAN)  |
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
    0x00, 0x00, 0x00, 0x00      // PropertyData – 0x00000003 (DShow Bridge is enabled and MJPEG is decoded in FrameServer)
}
```

### <a name="resources"></a>资源

[针对 USB 设备的 Microsoft OS 描述符](../usbcon/microsoft-defined-usb-descriptors.md)

[USB 常规父驱动程序 (Usbccgp.sys)](../usbcon/usb-common-class-generic-parent-driver.md)

[USB 规范](https://www.usb.org/documents)
