---
title: 支持环境光线传感器
description: 支持环境光线传感器
ms.assetid: a0875084-c093-4659-91b9-375450f65234
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f5b2eb7bf2c72f0e5e4e73c29f74050a19917ff3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56533858"
---
# <a name="supporting-ambient-light-sensors"></a>支持环境光线传感器


环境光线传感器可以测量当前光照条件。 从光线传感器的数据可用于自动调整屏幕亮度和键盘照明。 此外可以创建光感知的应用程序调整当前的光照条件的用户界面元素。 在 Windows 8 中，完全支持自动的亮度控制与环境光线传感器 （自适应亮度）。

Windows 8 中包含这两个 ACPI 3.0b 类驱动程序支持-符合和符合 hid 标准的环境光线传感器实现。 这意味着您不需要编写自定义驱动程序以支持环境光线传感器。 因为这些驱动程序与 Windows 传感器和位置平台集成，还可以基于传感器 API 的客户端应用程序，使用这些传感器。

有关环境光线传感器和 Windows 8 中的自适应亮度功能的详细信息，请参阅白皮书"使用 Windows 10 集成环境的光线传感器"上[Windows 硬件开发人员中心](https://docs.microsoft.com/windows-hardware/design/whitepapers/integrating-ambient-light-sensors-with-computers-running-windows-10-creators-update)网站。

对于不是 ACPI 3.0b 的环境光线传感器的符合或符合 hid 标准的必须创建一个传感器驱动程序以与传感器和位置平台集成。

## <a name="handling-light-sensor-properties"></a>处理光线传感器属性


对于 Windows 8，正确的类型的传感器\_数据\_类型\_LIGHT\_级别\_LUX 是 VT\_R4。 但是，对于 Windows 7，正确的类型为 VT\_UI4。 因此，设备驱动程序需要正确处理这两种类型。

Windows 8 和 Windows 7 之间的差异的另一点是，早期 ALS 设备驱动程序应使用传感器\_属性\_更改\_敏感度要传递单个值而不是一组值中**IPortableDeviceValues**对象。

下面的伪代码演示如何正确处理可能的类型的传感器\_数据\_类型\_LIGHT\_级别\_LUX。

```cpp
SetLuxChangeSensitivity(PROPVARIANT var)
{
    if (var.vt == VT_UNKNOWN)
    {
        CComPtr<IPortableDeviceValues> spValues;
        PROPVARIANT entry;

        //
        // Var is a pointer to an IPortableDeviceValues
        // container. Cast and iterate through its entries.
        //

        spValues = static_cast<IPortableDeviceValues*>(pVar->punkVal);

        foreach entry in spValues
        {
            //
            // Note: omitting check for SENSOR_DATA_TYPE_LIGHT_LEVEL_LUX key
            //

            if (entry.vt == VT_R4)
            {
                //
                // VT_R4 is the expected type for
                // SENSOR_DATA_TYPE_LIGHT_LEVEL_LUX.
                // Reference entry.fltVal.
                //
            }
            else if (entry.vt == VT_UI4)
            {
                //
                // VT_UI4 is deprecated, but use it anyway.
                // Reference entry.ulVal.
                //
            }
            else
            {
                //
                // All other types are invalid.
                // Return an error accordingly.
                //
            }
        }
    }
    else if (var.vt == VT_UI4)
    {
        //
        // Top level type of VT_UI4 is deprecated for
        // SENSOR_PROPERTY_CHANGE_SENSITIVITY, but use it anyway.
        // Reference entry.ulVal.
        //
    }
    else
    {
        //
        // All other types are invalid.
        // Return an error accordingly.
        //
    }
}
```

## <a name="related-topics"></a>相关主题

[传感器驱动程序开发的基础知识](sensor-driver-development-basics.md)



