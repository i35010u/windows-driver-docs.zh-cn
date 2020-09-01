---
title: 基于 SoC 的平台的硬件要求
description: ACPI 5.0 规范引入了一组新的硬件要求，以支持运行 Windows 的基于 SoC 的平台。
ms.assetid: C8AA4EE1-D9A6-438E-801B-8EDDF8AA0560
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f92be409690ea569d1f9dd5097b540a0bec56620
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89189002"
---
# <a name="hardware-requirements-for-soc-based-platforms"></a>基于 SoC 的平台的硬件要求


[ACPI 5.0 规范](https://uefi.org/specifications)引入了一组新的硬件要求，以支持运行 Windows 的基于 SoC 的平台。 ACPI 5.0 支持硬件降低的系统设计以降低成本，并支持连接待机电源型号，以延长电池寿命。

## <a name="hardware-reduced-acpi-platforms"></a>硬件-减少了 ACPI 平台


为了支持 Soc，Windows 不需要硬件平台来实现 ACPI 5.0 规范第4章 "ACPI 硬件规范" 中所述的任何功能。 无需 ACPI 固定硬件功能，如下所示：

-   电源管理 (PM) 计时器
-   实时时钟 (RTC) 唤醒警报
-   系统控制中断 (科幻) 
-   固定硬件注册集 (PMx \_ \* 事件/控制/状态寄存器) 
-   GPE 块注册 (GPEx \_ \* 事件/控制/状态寄存器) 
-   嵌入式控制器

未实现 ACPI 固定硬件接口的平台称为 *硬件精简* acpi 平台。 若要指示某个平台硬件已降低，请 \_ \_ 在 "固定 ACPI 说明" 表中设置 "HW 缩减 acpi" 标志 (FADT) "。

在硬件上，降低了 ACPI 平台，固定硬件功能（如 *电源按钮*、 *盖子状态*等）在 acpi 定义的硬件中一直被实现，由其 acpi 定义的软件等效项替换。 例如，使用控制方法的 "电源" 按钮而不是固定硬件等效项。

## <a name="connected-standby"></a>连接待机


用于实现连接待机电源型号的平台 (InstantGo 设备的一项重要功能) 作为提供在 ACPI 5.0 中定义的低功耗 S0 空闲功能的平台向 Windows 公开。 必须将 FADT 中的 "低功耗 S0 空闲" 标志设置为指示该平台支持连接待机。

Windows 支持具有低功耗 S0 空闲功能的平台，无论它们是实现硬件缩减的 ACPI 还是完全 ACPI。 但是，根据 ACPI 5.0 规范的要求，无论 ACPI 配置如何，Windows 也不会在具有低功耗 S0 空闲功能的平台上使用传统睡眠/恢复功能。

有关连接备用电源模式的详细信息，请参阅 [新式备用](/previous-versions/dn915061(v=vs.85))。

## <a name="acpi-events"></a>ACPI 事件


作为 ACPI 5.0 规范的第4章 "ACPI 硬件规范" 的一部分，定义了一个功能完备的机制，用于通知硬件事件。 Windows 支持规范中定义的多个事件，此支持将传输到 SoC 平台。 但是，对于硬件缩减的 ACPI 平台，GPIO 中断用于向事件发出信号，而不是由 ACPI 定义的 GPE/科幻硬件提供信号。 发出事件信号后，事件处理在硬件缩减和完整 ACPI 平台之间完全相同。 在这两种情况下，ACPI 指定的事件处理机制将调用相应的控件方法 (处理程序) 事件，最终将 ACPI 定义的通知发送到适当的设备驱动程序。

有关 GPIO 终止的 ACPI 事件的详细信息，请参阅 ACPI 5.0 规范的 "GPIO 终止的 ACPI 事件" 部分。 有关 ACPI 软件事件处理的详细信息，请参阅 ACPI 5.0 规范的 5.6.4 "常规用途事件处理" 部分。

 

