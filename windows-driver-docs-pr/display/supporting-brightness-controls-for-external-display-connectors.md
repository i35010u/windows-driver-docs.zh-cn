---
title: 外部显示器连接器的亮度控制
description: 此功能仅使 Oem 可以指示 Windows 到外部连接器显示支持的亮度控制。
keywords:
- WDK 显示亮度
- 基于 ACPI 亮度热键 WDK 显示
- 通知 WDK 显示亮度热键
- BIOS 亮度控制 WDK 显示
- 自动亮度 WDK 显示
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: 33a85da16641344aea282f7ffff9ec8792220ee2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63375897"
---
# <a name="brightness-controls-for-external-display-connectors"></a>外部显示器连接器的亮度控制

某些 OEM 系统具有使用 HDMI 等外部连接器连接的内部显示。 对于这些配置，Windows 已将指定一个显示面板，以支持系统软件亮度控制的功能。
此功能仅使 Oem 可以指示 Windows 到外部连接器显示支持的亮度控制;Oem 必须仍实现硬件亮度控制和集成的图形驱动程序，就像对于[集成的连接器显示](https://docs.microsoft.com/windows-hardware/drivers/display/supporting-brightness-controls-on-integrated-display-panels)。 此功能还不支持控制多个显示面板的各个面板亮度的功能。


### <a name="general-requirements"></a>一般要求

将添加一个新的 DWORD 注册表值："BrightnessControl"。
注册表路径：HKLM\SYSTEM\CurrentControlSet\Control\Class\{4D36E96E-E325-11CE-BFC1-08002BE10318} \XXXX 其中 XXXX 是为目标的单独显示。  


*   在此注册表值中的第一位定义非内部监视器亮度控制支持。
*   第二个位定义强制 ACPI 亮度，以使用 ACPI 重写。
*   剩余 30bits 得到保留，并且必须为零。  

要启用非内部面板上的亮度控制的 Oem 必须提供其自己 monitor.inf (请参阅示例 inf 下面) 并相应地设置此注册表值。 

在需要时，Oem 应只能定义"BrightnessControl"注册表值。 

亮度支持控件重写 （第一位） 只应在显示的任何适配器内部连接器类型上没有以内部方式显示的系统上。 如果系统内部连接器类型具有以内部方式显示，第一个枚举的显示将收到的亮度控制。


### <a name="acpi-brightness-override"></a>ACPI 亮度重写

ACPI 亮度重写不是要使用的亮度控制的首选的机制，但为了保持完整性，在情况下为包括其中的亮度控制没有其他选项。

ACPI 重写 （第二个位） 在内部和外部显示器上有效，但必须只能应用于在系统上的一个显示。

ACPI 替代旨在是与亮度目标重写时，结合使用，并且只时显示驱动程序不提供亮度支持。  这使 Oem 可以实现自己的显示背景光控制通过 ACPI。 

亮度支持对移动系统，这种情况有几个常见原因失败时，对于 ACPI 重写第二个用途是在 OS/驱动程序开发过程。 在这种情况下，仅作为临时解决方案; 旨在 ACPI 重写驱动程序的亮度控制应应用于最终产品。

中的外部连接器将设置此注册表值的位置的情况下，OS 会限制到一个公开的亮度控制系统。


### <a name="sample-monitorinf-file-fragment"></a>示例监视器。INF 文件片段

下面是概括介绍了上述不完整的示例 INF:

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
> Oem 需要提供一个 monitor.inf 文件，以确保不使用泛型 Microsoft monitor.inf 具有适当的硬件 ID。 
