---
title: ACPI 设计指南
description: 本部分介绍了设备驱动程序如何与高级配置和电源接口 (ACPI) 设备进行交互。 ACPI 设备是由高级配置和电源接口 (ACPI) 规范定义的。
ms.assetid: 294f4b43-2b3e-4afa-8fa8-74a6719131c7
ms.date: 01/24/2018
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
---

# <a name="acpi-design-guide"></a>ACPI 设计指南


本部分介绍了设备驱动程序如何与高级配置和电源接口 (ACPI) 设备进行交互。 ACPI 设备是由[高级配置和电源接口 (ACPI) 规范](https://go.microsoft.com/fwlink/p/?linkid=866846)定义的。

## <a name="in-this-section"></a>本部分中的内容


| 部分 | 描述 |
| --- | --- |
| [支持 ACPI 设备](supporting-acpi-devices.md) | 介绍了如何使用 Windows 驱动模型 (WDM) 功能驱动程序增强 ACPI 设备的功能。 |
| [评估 ACPI 控制方法](evaluating-acpi-control-methods.md) | 介绍了符合[内核模式驱动程序框架 (KMDF)](https://docs.microsoft.com/windows-hardware/drivers/kernel)、[用户模式驱动程序框架 (UMDF)](https://docs.microsoft.com/windows-hardware/drivers/wdf/getting-started-with-umdf-version-2) 或 [Windows 驱动模型 (WDM)](https://docs.microsoft.com/windows-hardware/drivers/kernel/windows-driver-model) 的要求的设备驱动程序如何评估 ACPI 控制方法。 |
| [如何使用 _OSI 识别 ACPI 中的 Windows 版本](winacpi-osi.md) | 提供了用来识别主机操作系统的 ACPI 源语言 (ASL) 操作系统接口级别 (\_OSI) 方法的信息。 |


## <a name="related-sctions"></a>相关章节

-   [ACPI DDI 参考](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_acpi)

 



