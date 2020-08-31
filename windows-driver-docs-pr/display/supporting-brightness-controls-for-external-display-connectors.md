---
title: 支持外部显示连接器的亮度控件
description: 此功能仅允许 Oem 向 Windows 指示外部连接器显示支持亮度控制。
keywords:
- 亮度 WDK 显示
- 基于 ACPI 的亮度热键显示屏
- 通知亮度热键热键显示
- BIOS 亮度控制 WDK 显示
- 自动显示亮度 WDK
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: 60726633ca04cf691b3a9da262e3e6a5f36c5f16
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89063462"
---
# <a name="supporting-brightness-controls-for-external-display-connectors"></a>支持外部显示连接器的亮度控件

某些 OEM 系统具有使用外部连接器（如 HDMI）连接的内部显示器。 对于这些配置，Windows 能够仅指定一个显示面板来支持系统软件亮度控件。
此功能仅允许 Oem 向 Windows 指示外部连接器显示支持亮度控制;Oem 仍必须实现硬件亮度控件，并将其与图形驱动程序集成，就好像它们适用于 [集成连接器显示](./supporting-brightness-controls-on-integrated-display-panels.md)一样。 此功能也不支持在多个显示面板上控制各个面板亮度。

## <a name="general-requirements"></a>一般要求

将添加新的 DWORD 注册表值： "BrightnessControl"。
注册表路径： HKLM\SYSTEM\CurrentControlSet\Control\Class \{ 4D36E96E-E325-11CE-BFC1-08002BE10318} \XXXX，其中 XXXX 用于目标单个显示。  

* 此注册表值中的第一个位定义了非内部监视器亮度控件支持。
* 第二个位定义强制使用 ACPI 亮度的 ACPI 重写。
* 剩余的30bits 是保留的，并且必须为零。  

希望在非内部面板上启用亮度控制的 Oem 必须提供其自己的监视器。 inf (参阅下面) 的示例 inf，并适当地设置此注册表值。

Oem 只应在需要时定义 "BrightnessControl" 注册表值。

亮度支持控件覆盖 (第一位) 只应在不具有任何显示适配器上内部连接器类型内部显示的系统上使用。 如果系统对内部连接器类型具有内部显示，则第一个枚举的显示将接收亮度控件。

## <a name="acpi-brightness-override"></a>ACPI 亮度替代

ACPI 亮度替代不是用于亮度控制的首选机制，但出于完整性考虑，在没有其他选项可用于亮度控制时包含。

ACPI 替代 (第二个位) 在内部和外部显示器上都有效，但必须仅应用于系统上的一个显示。

ACPI 替代旨在与亮度目标替代结合使用，并且仅当显示驱动程序未提供亮度支持时使用。  这允许 Oem 通过 ACPI 实现其自己的显示背光控制。

ACPI 替代的辅助用途是在操作系统/驱动程序开发期间，如果移动系统上的亮度支持失败，则可能是由于几个常见原因导致的。 在这种情况下，ACPI 替代仅用作过渡解决方案;驱动程序亮度控件应用于已完成的产品。

如果为外部连接器设置了此注册表值，则 OS 会将系统限制为一个暴露的亮度控制。

## <a name="sample-monitorinf-file-fragment"></a>示例监视器。INF 文件片段

下面是一个未完成的示例 INF，其中概述了上述内容：

```inf
[Manufacturer]
%MONOEM%=MONOEM,NTx86,NTAMD64

[MONOEM]  
%AIOHDMI_1%  = AIO_HDMI_1, Monitor\OEM1001
%AIOHDMI_2%  = AIO_HDMI_2, Monitor\OEM1002
%Laptop%  = Laptop_1, Monitor\OEM2001

[MONOEM.NTx86]
%AIOHDMI_1%  = AIO_HDMI_1, Monitor\OEM1001
%AIOHDMI_2%  = AIO_HDMI_2, Monitor\OEM1002
%Laptop%  = Laptop_1, Monitor\OEM2001

[MONOEM.NTAMD64]  
%AIOHDMI_1%  = AIO_HDMI_1, Monitor\OEM1001
%AIOHDMI_2%  = AIO_HDMI_2, Monitor\OEM1002
%Laptop%  = Laptop_1, Monitor\OEM2001

[ControlFlags]
ExcludeFromSelect = *

[AIO_HDMI_1]
AddReg= AIO_HDMI_1_Driver_Brightness

[AIO_HDMI_2]
AddReg= AIO_HDMI_2_ACPI_Brightness

[Laptop_1]
AddReg=Laptop_ACPI_Driver_Brightness


; Override brightness to control the HDMI built into the all-in-one system under graphics driver control
[AIO_HDMI_1_Driver_Brightness]
HKR,,BrightnessControl,%REG_DWORD%,%OVERRIDE_BRIGHTNESS_TARGET%

; Override brightness to control the HDMI built into the all-in-one system under ACPI firmware control
[AIO_HDMI_2_ACPI_Brightness]
HKR,,BrightnessControl,%REG_DWORD%,%OVERRIDE_BRIGHTNESS_TARGET_AND_CONTROL_TO_ACPI%

; Override brightness to control the internal panel under ACPI firmware control instead of the driver
[Laptop_ACPI_Driver_Brightness]
HKR,,BrightnessControl,%REG_DWORD%,%OVERRIDE_BRIGHTNESS_CONTROL_TO_ACPI%

[Strings]
; Non-localizable
REG_DWORD = 0x00010001
OVERRIDE_BRIGHTNESS_TARGET = 1
OVERRIDE_BRIGHTNESS_CONTROL_TO_ACPI = 2
OVERRIDE_BRIGHTNESS_TARGET_AND_CONTROL_TO_ACPI = 3

; Localizable
MONOEM = “Manufacturer name”
AIOHDMI_1  = “AIO monitor name one”
AIOHDMI_2  = “AIO monitor name two”
Laptop  = “Laptop monitor name”
```

> [!NOTE]
> Oem 需要提供具有正确硬件 ID 的监视器 .inf 文件，以确保不使用一般的 Microsoft monitor。