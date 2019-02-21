---
title: PCI 电源管理和设备驱动程序
description: 阐明了符合 PCI 电源管理 (PCI PM) 的硬件与设备驱动程序之间的交互。
ms.assetid: BA6792EE-CAD8-4C9E-AAA6-D1D8799F50C3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dba043ac0e4b9df2d7ebbe2cb836ce14d0d7bfc6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56545122"
---
# <a name="pci-power-management-and-device-drivers"></a>PCI 电源管理和设备驱动程序


**已更新**

-   2001 年 12 月 4日日

本文阐明了供应商有关符合 PCI 电源管理 (PCI PM) 的硬件与操作系统中的设备驱动程序之间的交互以及如何与 ACPI 集成 PCI PM 遇到的一些混淆。 有关详细信息，请参阅<https://www.uefi.org/specifications>

## <a name="device-drivers-and-pci-power-management"></a>设备驱动程序和 PCI 的电源管理


本文假设你不熟悉 Windows 驱动程序模型 (WDM) 驱动程序如何处理电源管理事件，如当前 Windows DDK 中所述。 一般情况下，设备驱动程序的职责如下所示：

-   **总线驱动程序**:总线驱动程序负责枚举、 配置和控制设备。 对于 PCI PM PCI 驱动程序负责读取 PCI PM 寄存器来确定硬件的功能。 当 POWER Irp 请求电源状态更改时，PCI 驱动程序将写入到 PCI 电源管理寄存器将硬件设置为不同的 Dx 状态。

    PCI 驱动程序时唤醒启用了设备，写入 PCI PM 寄存器，要使设备能够激发 PME (ACPI 还采取措施，请参阅下一部分)。 最后，当 ACPI 确定 PCI 总线唤醒系统时，PCI 驱动程序将扫描 PCI 寻找哪些设备断言 PME、 禁用 PME 中该设备，并通知该设备的驱动程序的配置空间。

-   **设备驱动程序**:设备的特定驱动程序是负责保存和还原设备上下文，并请求为该设备的策略所有者的电源状态更改。 当设备驱动程序收到请求较低的设备电源状态更改 POWER IRP 时，设备驱动程序负责保存更高版本打开设备所需的任何专有设备上下文。 在某些情况下，可能没有要保存的内容。

域严格的 PCI PM 寄存器的 PCI 驱动程序，IHV 的设备驱动程序不需要访问任何这些寄存器。 执行此操作会导致系统无法可靠工作。 设备驱动程序的责任是执行仅专有操作。

## <a name="integrating-acpi-and-pci-pm"></a>集成 ACPI 和 PCI PM


某些设备，尤其是母板在笔记本电脑上，视频设备可能需要同时 PCI 电源管理，以及 ACPI 源语言组装器 (ASL) 完全的电源管理设备。 PCI 电源管理寄存器将控制的设备，如内部时钟和 power 平面的内部状态。 ASL 将控制的外部状态，例如外部时钟和 power 平面或 ASL 会在视频控制器的情况下控制视频的背光功能。 请注意，PCI 5:15AM、5:45AM、5:15PM 和 ASL 仅可以组合在主板设备上。

OnNow 体系结构是分层体系结构，自然地处理的设备驱动程序、 PCI 驱动程序和 ACPI 驱动程序 （和 ASL） 集成。 以下方案显示驱动程序将调用以处理这些设备的顺序。

**请注意**  对于上面的方案所述，WDM 驱动程序必须将转发 POWER Irp 当前版本的 Microsoft Windows DDK 中所述正确。

 

## <a name="scenario-1-turning-off-a-device"></a>方案 1：关闭设备


1.  **设备驱动程序**:保存专用设备状态。
2.  **PCI 驱动程序**:保存插配置中，禁用的设备 （中断和条形图），并将放在 D3 使用 PCI PM 注册的设备。
3.  **ACPI 驱动程序**:运行 ASL 代码 (\_PS3 和\_电源中的资源不能再使用 OFF) 来控制外部的芯片的状态。

## <a name="scenario-2-pci-power-management-and-device-drivers"></a>方案 2：PCI 电源管理和设备驱动程序


1.  **ACPI 驱动程序**:运行 ASL 代码 (\_PS0 和\_对任何 OnNow 所需的能源) 来控制外部的芯片的状态。
2.  **PCI 驱动程序**:让使用 PCI PM 寄存器中 D0 设备并将还原插配置 （中断和条-这些可能不同于什么设备上的以前）。
3.  **设备驱动程序**:还原的设备中的专用上下文。

## <a name="scenario-3-enabling-wake-up"></a>方案 3：启用唤醒


1.  **设备驱动程序**:设置专用寄存器中芯片以启用唤醒。 例如，在模式匹配网络唤醒，这，是到该适配器会对编程模式时。
2.  **PCI 驱动程序**:设置唤醒启用 bits 以允许设备进行断言 PME PCI PM 寄存器中。
3.  **ACPI 驱动程序**:启用 PME 与关联的芯片集在 GPE (如中所述\_PRW 对象列出根 PCI 总线下)。

## <a name="scenario-4-wake-up"></a>方案 4:唤醒


1.  **ACPI 驱动程序**:唤醒并扫描唤醒事件，并为集 GPE 状态位，禁用 GPEs 和运行任何 GPE 状态位\_Lxx 或\_Exx 方法设置 GPE 位与相关联。 ACPI 驱动程序将在响应唤醒通知 PCI 总线上，完成 PCI 驱动程序等待\_唤醒 IRP，以通知 PCI 驱动程序，它唤醒系统。
2.  **PCI 驱动程序**:扫描正在查找与设置 PME 状态位的任何设备的配置空间。 对于每个设备，它禁用 PME 并完成等待\_该设备的唤醒 IRP，以通知断言唤醒驱动程序。 PCI 驱动程序将停止扫描唤醒设备时通过所有 PCI 设备具有未找到任何断言 PME 和 PME 停止断言时，已完成传递。
3.  **设备驱动程序**:请求设备置于 D0 （请参阅方案 2），并在处理唤醒事件所需的芯片中设置任何专有寄存器。

## <a name="call-to-action-on-pci-power-management-and-device-drivers"></a>行动号召 PCI 电源管理和设备驱动程序：


-   在本文中所述，将 ACPI 和 PCI PM 功能集成到你的设备。
-   PCI 电源管理规范位于<http://www.pcisig.com>。 此链接将离开 Microsoft.com 网站。
-   ACPI 规范可在<https://www.uefi.org/specifications>。 此链接将离开 Microsoft.com 网站。
-   ACPI 组件体系结构 (ACPICA) 编译器可以找到在<https://acpica.org/downloads/binary-tools>。 此链接将离开 Microsoft.com 网站。

 

 




