---
title: ACPI 描述符示例
description: 本主题包含 ACPI 描述符示例。
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: e38807c6ab150ada66fd8a842e1028ab7f2437f4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96827197"
---
# <a name="acpi-descriptor-samples"></a>ACPI 描述符示例


本主题包含 ACPI 描述符示例。

**注意**  对于设备定义 (（例如 ") "），ACPI 描述符使用的长度只有4个字符。

 

## <a name="span-idacpi_description_for_button_arrayspanspan-idacpi_description_for_button_arrayspanspan-idacpi_description_for_button_arrayspanacpi-description-for-button-array"></a><span id="ACPI_description_for_button_array"></span><span id="acpi_description_for_button_array"></span><span id="ACPI_DESCRIPTION_FOR_BUTTON_ARRAY"></span>按钮数组的 ACPI 说明


``` syntax
Device(BTT00N)
{
    Method(_HID, 0x0, NotSerialized)
    {
        Return("ID9000")
    }
        Name(_CID, "PNP0C40")
        Name(_CRS, ResourceTemplate()
                {
                GpioInt(Edge, 
                        ActiveLow, 
                        SharedAndWake, 
                        PullDefault, 
                        0, "\\_SB.GPIO", 
                        0, ResourceConsumer, , 
                        RawDataBuffer() {}) 
                 {0xE1}
                GpioInt(Edge, 
                        ActiveBoth, 
                        SharedAndWake, 
                        PullDefault, 
                        0, "\\_SB.GPIO", 
                        0, ResourceConsumer, , 
                        RawDataBuffer() {}) 
                {0xE2}
                GpioInt(Edge, 
                        ActiveBoth, 
                        Exclusive, 
                        PullDefault, 
                        0, "\\_SB.GPIO", 
                        0, ResourceConsumer, , 
                        RawDataBuffer() {}) 
                {0xE3}
                GpioInt(Edge, 
                        ActiveBoth, 
                        Exclusive, 
                        PullDefault, 
                        0, "\\_SB.GPIO", 
                        0, ResourceConsumer, , 
                        RawDataBuffer() {}) 
                {0xE4}
                GpioInt(Edge, 
                        ActiveBoth, 
                        Exclusive, 
                        PullDefault, 
                        0, "\\_SB.GPIO", 
                        0, ResourceConsumer, , 
                        RawDataBuffer() {}) 
                {0xE5}
                })
}
```

## <a name="span-idacpi_description_for_laptop_slate_mode_indicatorspanspan-idacpi_description_for_laptop_slate_mode_indicatorspanspan-idacpi_description_for_laptop_slate_mode_indicatorspanacpi-description-for-laptopslate-mode-indicator"></a><span id="ACPI_description_for_laptop_slate_mode_indicator"></span><span id="acpi_description_for_laptop_slate_mode_indicator"></span><span id="ACPI_DESCRIPTION_FOR_LAPTOP_SLATE_MODE_INDICATOR"></span>笔记本电脑/石板模式指示器的 ACPI 说明


``` syntax
Device(CONV)
{
    Method(_HID, 0x0, NotSerialized)
        {
            Return("ID9001")
        }
     Name(_CID, "PNP0C60")
}
```

## <a name="span-idacpi_description_for_docking_mode_indicatorspanspan-idacpi_description_for_docking_mode_indicatorspanspan-idacpi_description_for_docking_mode_indicatorspanacpi-description-for-docking-mode-indicator"></a><span id="ACPI_description_for_docking_mode_indicator"></span><span id="acpi_description_for_docking_mode_indicator"></span><span id="ACPI_DESCRIPTION_FOR_DOCKING_MODE_INDICATOR"></span>停靠模式指示器的 ACPI 说明


``` syntax
Device(DOCK)
{
    Method(_HID, 0x0, NotSerialized)
    {
        Return("ID9002")
     }
     Name(_CID, "PNP0C70")
}
```

 

 




