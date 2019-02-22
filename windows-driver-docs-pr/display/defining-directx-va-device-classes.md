---
title: 定义 DirectX VA 设备类
description: 定义 DirectX VA 设备类
ms.assetid: a4b2ee88-747a-48c3-ba1d-2d605c46db58
keywords:
- DirectX 视频加速 WDK Windows 2000 显示中，定义设备类别
- 设备类 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b1a95ad517c67d0ec418cfafc4d99749eca8e0ed
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56534378"
---
# <a name="defining-directx-va-device-classes"></a>定义 DirectX VA 设备类


## <span id="ddk_defining_directx_va_device_classes_gg"></span><span id="DDK_DEFINING_DIRECTX_VA_DEVICE_CLASSES_GG"></span>


使用本节中的示例代码来定义用于取消隔行扫描容器设备、 ProcAmp 控制设备、 取消隔行扫描模式设备的设备类 (例如， [bob](bob-deinterlacing.md))，和 COPP 设备。 这些设备类包含声明的成员函数，构成[ProcAmp 控件 DDI](https://msdn.microsoft.com/library/windows/hardware/ff569186)并[取消隔行扫描 DDI](https://msdn.microsoft.com/library/windows/hardware/ff552701)。 可以在驱动程序所提供的标头文件中声明这些设备类定义。

下面的示例代码用于定义每种设备类型和适用于每种设备类型的基类：

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

以下主题包含定义取消隔行扫描容器设备、 ProcAmp 控制设备、 取消隔行扫描 bob 设备和 COPP 设备类的示例代码：

[定义取消隔行扫描容器设备类](defining-the-deinterlace-container-device-class.md)

[定义 ProcAmp 控制设备类](defining-the-procamp-control-device-class.md)

[定义取消隔行扫描 Bob 设备类](defining-the-deinterlace-bob-device-class.md)

[定义 COPP 设备类](defining-the-copp-device-class.md)

 

 





