---
title: Uvc 控件缓存的驱动程序支持
description: 提供有关如何显式利用设备的照相机控件缓存的信息。
ms.date: 08/16/2019
ms.localizationpriority: medium
ms.openlocfilehash: 37b39543f8000d5cf4256dfa22d0f975ad0f457b
ms.sourcegitcommit: dff3834724bd5204c4a47204540fe8125dd37b20
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/06/2019
ms.locfileid: "70775185"
---
# <a name="driver-support-for-camera-uvc-control-cache"></a>相机 UVC 控件缓存的驱动程序支持

框架服务器关闭时，UVC 控制设备上的控件。 如果一个应用使用 UVC 控件设置白平衡，然后关闭应用，则不会重置照相机的白平衡。 打开且不更改白平衡的其他应用将继承以前的设置。

一种例外情况是计算机进入 S3 时。 根据相机设备是否进入 D3 或 D3 冷，UVC 控件会分别出现，也可能不会。 此行为是因为 D3 冷消除了照相机电源。

利用 Cache UVC Control 协议，可以在应用程序会话、S3 和计算机关闭之间保持一致的行为。
  
通过将配置项 "CacheUVCControl" 设置为 "设备 HW" 注册表项中的 DWORD 值1，通过 MS OS 2.0 描述符或较旧的自定义 INF 文件方法，照相机会保留用户跨 S3 或计算机重启设置的 UVC 控制值。 将存储和重新应用的特定 UVC 控件值的列表如下所示。

## <a name="uvc-controls-affected"></a>受影响的 UVC 控件

下面是一个 UVC 控件列表，这些控件将在重新启动时进行缓存和重新应用：

- KSPROPERTY_VIDEOPROCAMP_BRIGHTNESS
- KSPROPERTY_VIDEOPROCAMP_CONTRAST
- KSPROPERTY_VIDEOPROCAMP_GAIN
- KSPROPERTY_VIDEOPROCAMP_GAMMA
- KSPROPERTY_VIDEOPROCAMP_HUE （+ AUTO）
- KSPROPERTY_VIDEOPROCAMP_SATURATION
- KSPROPERTY_VIDEOPROCAMP_SHARPNESS
- KSPROPERTY_VIDEOPROCAMP_WHITEBALANCE （+ AUTO）

## <a name="inf-example"></a>INF 示例

```cpp
[Device.AddReg.HW]
HKR,,"CacheUVCControl",0x00010001,1
```

## <a name="ms-os-20-descriptor-example"></a>MS OS 2.0 描述符示例

```cpp
UCHAR Example_MSOS20DescriptorSet_CacheUVCControl[0x38] =
{
    //
    // Microsoft OS 2.0 Descriptor Set Header
    //
    0x0A, 0x00,               // wLength - 10 bytes
    0x00, 0x00,               // MSOS20_SET_HEADER_DESCRIPTOR
    0x00, 0x00, 0x0?, 0x06,   // dwWindowsVersion – 0x060?0000 for future Windows version
    0x3C, 0x00,               // wTotalLength – 60 bytes

    //
    // Microsoft OS 2.0 Registry Value Feature Descriptor
    //
    0x32, 0x00,               // wLength 0x32 (50) in bytes of this descriptor  
    0x04, 0x00,               // wDescriptorType – MSOS20_FEATURE_REG_PROPERTY  
    0x04, 0x00,               // wPropertyDataType - REG_DWORD  
    0x24, 0x00,               // wPropertyNameLength – 0x24 (36) bytes
    'C',  0x00, 'a',  0x00,   // Property Name - “CacheUVCControl”  
    'c',  0x00, 'h',  0x00,  
    'e',  0x00, 'U',  0x00,
    'V',  0x00, 'C',  0x00,  
    'C',  0x00, 'o',  0x00,  
    'n',  0x00, 't',  0x00,  
    'r',  0x00, 'o',  0x00,  
    'l',  0x00, 0x00, 0x00,
    0x00, 0x00, 0x00, 0x00,
    0x04, 0x00,               // wPropertyDataLength – 4 bytes  
    0x01, 0x00, 0x00, 0x00,   // Enable to cache UVC controls  
}
```
