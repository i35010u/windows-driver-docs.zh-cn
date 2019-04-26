---
title: ACPI 描述符示例
description: 本主题包含 ACPI 描述符的示例。
ms.assetid: E091DF59-2E9F-4652-801C-3F55CBB910FE
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 9d1badd6c1aee7326d4584df13203f6bd0eb9d58
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63326119"
---
# <a name="acpi-descriptor-samples"></a>ACPI 描述符示例


本主题包含 ACPI 描述符的示例。

**请注意**  使用仅有的 4 个字符长度 （如 CONV) 的设备定义的 ACPI 描述符。

 

## <a name="span-idacpidescriptionforbuttonarrayspanspan-idacpidescriptionforbuttonarrayspanspan-idacpidescriptionforbuttonarrayspanacpi-description-for-button-array"></a><span id="ACPI_description_for_button_array"></span><span id="acpi_description_for_button_array"></span><span id="ACPI_DESCRIPTION_FOR_BUTTON_ARRAY"></span>针对按钮阵列的 ACPI 描述


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

## <a name="span-idacpidescriptionforlaptopslatemodeindicatorspanspan-idacpidescriptionforlaptopslatemodeindicatorspanspan-idacpidescriptionforlaptopslatemodeindicatorspanacpi-description-for-laptopslate-mode-indicator"></a><span id="ACPI_description_for_laptop_slate_mode_indicator"></span><span id="acpi_description_for_laptop_slate_mode_indicator"></span><span id="ACPI_DESCRIPTION_FOR_LAPTOP_SLATE_MODE_INDICATOR"></span>便携式计算机/盖板模式指示器的 ACPI 描述


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

## <a name="span-idacpidescriptionfordockingmodeindicatorspanspan-idacpidescriptionfordockingmodeindicatorspanspan-idacpidescriptionfordockingmodeindicatorspanacpi-description-for-docking-mode-indicator"></a><span id="ACPI_description_for_docking_mode_indicator"></span><span id="acpi_description_for_docking_mode_indicator"></span><span id="ACPI_DESCRIPTION_FOR_DOCKING_MODE_INDICATOR"></span>针对停靠模式指示器 ACPI 描述


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

 

 




