---
title: 支持环境光线传感器
description: 支持环境光线传感器
ms.assetid: a0875084-c093-4659-91b9-375450f65234
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3bffad4aeb800db391c344bfe3b063cdbd5b8b3e
ms.sourcegitcommit: b75e9940d49410e2b952e96f325df67a039cd571
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/21/2020
ms.locfileid: "92337048"
---
# <a name="supporting-ambient-light-sensors"></a>支持环境光线传感器

环境光线传感器可以度量当前照明条件。 可以使用光线传感器的数据自动调整屏幕亮度和键盘照明。 您还可以创建用于调整当前照明条件的用户界面元素的光源感知应用程序。 在 Windows 8 中，具有环境光线传感器的自动亮度控制 (完全支持自适应亮度) 。

Windows 8 为 ACPI 3.0 b 兼容和符合 HID 标准的环境光线传感器实现提供类驱动程序支持。 这意味着你无需编写自定义驱动程序来支持环境光线传感器。 这些传感器还可以由基于传感器 API 的客户端应用程序使用，因为这些驱动程序与 Windows 传感器和位置平台集成。

有关环境光线传感器和 Windows 8 中的自适应亮度功能的详细信息，请参阅 [Windows 硬件开发人员中心](/windows-hardware/design/whitepapers/integrating-ambient-light-sensors-with-computers-running-windows-10-creators-update) 网站上的白皮书 "将环境光线传感器与 Windows 10 集成"。

对于不符合 ACPI 3.0 b 或符合 HID 标准的环境光线传感器，你必须创建一个传感器驱动程序以与传感器和位置平台集成。

## <a name="handling-light-sensor-properties"></a>处理光传感器属性

对于 Windows 8，传感器 \_ 数据 \_ 类型 \_ 轻型级别 LUX 的正确 \_ 类型 \_ 是 VT \_ R4。 但对于 Windows 7，正确的类型为 VT \_ UI4。 因此，设备驱动程序需要正确处理这两种类型。

Windows 8 和 Windows 7 之间的另一个区别在于，较早的 ALS 设备驱动程序预期的传感器 \_ 属性 \_ 更改 \_ 敏感度应作为单个值（而不是 **IPortableDeviceValues** 对象中的一组值）传递。

下面的伪代码演示了如何正确处理传感器 \_ 数据 \_ 类型 \_ 轻型 \_ 级别 \_ LUX 的可能类型。

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

[传感器驱动程序逻辑](/windows-hardware/drivers/sensors/driver-logic--pseudo-code-)
