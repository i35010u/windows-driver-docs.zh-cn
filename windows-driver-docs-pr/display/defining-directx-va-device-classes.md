---
title: 定义 DirectX VA 设备类
description: 定义 DirectX VA 设备类
ms.assetid: a4b2ee88-747a-48c3-ba1d-2d605c46db58
keywords:
- DirectX 视频加速 WDK Windows 2000 显示，定义设备类
- 设备类 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3d2153fb633a240d1935dcc1321644e323e723c8
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89064336"
---
# <a name="defining-directx-va-device-classes"></a>定义 DirectX VA 设备类


## <span id="ddk_defining_directx_va_device_classes_gg"></span><span id="DDK_DEFINING_DIRECTX_VA_DEVICE_CLASSES_GG"></span>


使用本部分中的示例代码来定义隔行扫描容器设备、ProcAmp 控制设备、逐行扫描模式设备 (例如， [bob](bob-deinterlacing.md)) 和 COPP 设备的设备类。 这些设备类包含成员函数的声明，这些成员函数包含 [ProcAmp 控件 ddi](./procamp-control-ddi.md) 和取消 [隔行扫描](./deinterlace-ddi.md)。 可以在驱动程序提供的标头文件中声明这些设备类定义。

使用以下示例代码定义每种设备类型和适用于每种设备类型的基类：

```cpp
// These enumerated types specify the DirectX VA device class.
enum DXVA_DeviceType {
    DXVA_DeviceContainer        = 0x0001,
    DXVA_DeviceDecoder          = 0x0002,
    DXVA_DeviceDeinterlacer     = 0x0003,
     DXVA_DeviceProcAmpControl   = 0x0004,
    DXVA_DeviceCOPP             = 0x0005
};
// Other DirectX VA device classes inherit from this base class, 
struct DXVA_DeviceBaseClass {
    GUID            m_DeviceGUID;
    DXVA_DeviceType m_DeviceType;

    DXVA_DeviceBaseClass(const GUID& guid, DXVA_DeviceType Type) :
        m_DeviceGUID(guid), m_DeviceType(Type)
    {}
};
```

以下主题包含用于为隔行扫描容器设备、ProcAmp 控制设备、隔行扫描 bob 设备和 COPP 设备定义类的代码示例：

[定义反交错容器设备类](defining-the-deinterlace-container-device-class.md)

[定义 ProcAmp 控制设备类](defining-the-procamp-control-device-class.md)

[定义反交错 Bob 设备类](defining-the-deinterlace-bob-device-class.md)

[定义 COPP 设备类](defining-the-copp-device-class.md)

 

