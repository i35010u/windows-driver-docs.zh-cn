---
title: 基于 SoC 的平台的硬件要求
description: ACPI 5.0 规范引入了一组新的硬件要求，以支持运行 Windows 的基于 SoC 的平台。
ms.assetid: C8AA4EE1-D9A6-438E-801B-8EDDF8AA0560
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c3504315b3a3aa87a1188b0736ca39549619ade9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67364545"
---
# <a name="hardware-requirements-for-soc-based-platforms"></a>基于 SoC 的平台的硬件要求


[ACPI 5.0 规范](https://uefi.org/specifications)引入了一组新的硬件要求，以支持运行 Windows 的基于 SoC 的平台。 ACPI 5.0 支持硬件减少系统设计，以降低成本，并支持连接待机电源模型以启用长的电池使用寿命。

## <a name="hardware-reduced-acpi-platforms"></a>硬件减少 ACPI 平台


若要支持 Soc，Windows 不需要硬件平台，可以在第 4 章"ACPI 硬件规范"ACPI 5.0 规范的实现任何所述的功能。 修复了如下所示的硬件功能的 ACPI 不是必需的：

-   电源管理 (PM) 计时器
-   实时时钟 (RTC) 唤醒警报
-   系统控制中断 (SCI)
-   固定的硬件集注册 (PMx\_ \*事件/控件/状态注册)
-   GPE 块注册 (GPEx\_ \*事件/控件/状态注册)
-   嵌入式的控制器

未实现 ACPI 固定硬件接口的平台嘿 *硬件减少*ACPI 平台。 若要指示一个平台，是硬件减少，设置 HW\_减少了\_ACPI 标志中固定 ACPI 描述表 (FADT)。

硬件减少 ACPI 在平台上，如修复硬件功能*电源按钮*，*盖子状态*，依此类推，已在 ACPI 定义的硬件中实现传统上，以独占方式替换通过它们 ACPI 定义的软件的等效项。 例如，控件方法电源按钮使用而不是固定的硬件等效。

## <a name="connected-standby"></a>连接待机


实现连接待机电源模型 （InstantGo 设备的一个重要功能） 的平台将作为提供低能耗空闲 S0 功能在 ACPI 5.0 中定义的平台公开到 Windows。 必须设置 FADT 中的"低电源 S0 空闲能够"标志以指示该平台支持连接待机状态。

Windows 支持具有低能耗空闲 S0 功能而不考虑它们实现硬件减少 ACPI 或完整 ACPI 的平台。 但是，根据 ACPI 5.0 规范的要求，Windows 不使用具有低能耗空闲 S0 功能，而不考虑 ACPI 配置的平台上传统睡眠/恢复功能。

有关连接待机电源模型的详细信息，请参阅[现代备用](https://docs.microsoft.com/previous-versions/dn915061(v=vs.85))。

## <a name="acpi-events"></a>ACPI 事件


ACPI 5.0 规范的第 4，"ACPI 硬件规范"章的一部分为信号硬件事件定义了全功能的机制。 Windows 支持多个事件规范中定义，这种支持将传递给 SoC 平台。 但是，对于硬件减少 ACPI 平台，GPIO 中断用于发出信号的事件，而不是 ACPI 定义 GPE/SCI 硬件。 但是发出事件的信号后，事件处理是硬件减少和完整 ACPI 平台之间完全相同。 在这两种情况下，ACPI 指定事件处理机制，事件最终将 ACPI 定义的通知发送到相应的设备驱动程序调用相应的控件的方法 （处理程序）。

有关 GPIO 信号 ACPI 事件的详细信息，请参阅 ACPI 5.0 规范 5.6.5，"GPIO-Signaled ACPI 事件"部分。 有关处理的 ACPI 软件事件的详细信息，请参阅部分 5.6.4，"常规用途的事件处理"，ACPI 5.0 规范。

 

 




