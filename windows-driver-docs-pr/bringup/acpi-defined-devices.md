---
title: ACPI 定义的设备
description: ACPI 5.0 规范定义了许多用于表示和控制典型平台功能的设备类型。
ms.assetid: 10BD17C9-E8FE-41E0-BD8C-E622B60E6BB6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bea222904b76ab9ccc782d50cb31308310d7871a
ms.sourcegitcommit: b316c97bafade8b76d5d3c30d48496915709a9df
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/13/2020
ms.locfileid: "79242840"
---
# <a name="acpi-defined-devices"></a>ACPI 定义的设备


[ACPI 5.0 规范](https://uefi.org/specifications)定义了许多用于表示和控制典型平台功能的设备类型。 例如，ACPI 定义 "电源" 按钮、"睡眠" 按钮和 "系统指示器"。 对于基于 SoC 的平台，Windows 提供内置驱动程序来支持本文中所述的 ACPI 定义的设备。

有关详细信息，请参阅 ACPI 5.0 规范中的第9部分 "ACPI 定义的设备和特定于设备的对象"。

## <a href="" id="lid"></a>盖子设备


此设备描述并报告 clamshell 设备的盖子状态。 有关详细信息，请参阅[ACPI 5.0 规范](https://uefi.org/specifications)中的9.4 节 "控制方法盖子设备"。 盖子设备实现使用在 ACPI 5.0 规范中的5.6.5，"GPIO 终止的 ACPI 事件" 部分中所述的 GPIO 信号 ACPI 事件机制。

## <a href="" id="battery"></a>控制方法电池设备


此设备描述、配置和报告平台电池的状态。 有关详细信息，请参阅[ACPI 5.0 规范](https://uefi.org/specifications)中的10.2 节 "控制方法电池"。 用于 SoC 平台上的控制方法电池实现使用在 ACPI 5.0 规范中的5.6.5，"GPIO 终止的 ACPI 事件" 部分中所述的 GPIO 信号 ACPI 事件机制。 可以通过使用 GPIO 或 SPB OpRegions 操作的方法来访问电池和充电硬件，如 ACPI 5.0 规范的5.5.2.4.4 和5.5.2.4.5 部分中所述。

有关 Windows 中的电池管理的详细信息，请参阅[Windows 电源和电池子系统要求](https://docs.microsoft.com/windows-hardware/design/device-experiences/windows-power-and-battery-subsystem-requirements)。

**特定于电池设备的方法（\_DSM）**

为了支持平台被动热量管理，Microsoft 定义了一个 \_DSM 方法，用于与平台固件通信，这是由电池热区设置的散热限制。 有关详细信息，请参阅以下内容：

-   [特定于电池设备的方法](battery-device-specific-method.md)
-   [热量区域](#thermal)

## <a href="" id="time"></a>控制方法时间和警报设备


ACPI 5.0 定义了可选的基于控制方法的时间和警报设备的操作和定义，该方法提供与硬件无关的抽象，并为实时时钟（RTC）提供了更可靠的替代方法。 有关详细信息，请参阅[ACPI 5.0 规范](https://uefi.org/specifications)中的9.15 节 "PC/AT RTC/CMOS 设备" 和第9.18 节 "时间和警报设备"。 如果标准 PC RTC 未实现或用作支持时间和警报设备的 RTC 硬件，则必须设置 FADT 的启动体系结构标志字段的 "CMOS RTC 不存在" 位。

对于支持 InstantGo 功能（和连接待机电源模式）的平台，需要时间和警报设备的时间功能。 这些功能可在系统电源转换期间保持时间信息，并跟踪时间，即使平台已关闭也是如此。 当使用不同的固件接口查询平台时间时，平台上的时间应一致。 例如，用于获取时间的 UEFI 调用应返回操作系统使用时间和警报设备获得的相同时间。

必须从与 UEFI 时间服务相同的时间源驱动时间和警报设备。

## <a href="" id="thermal"></a>热量区域


为了支持 ACPI 热量管理，系统设计器会将硬件平台以逻辑方式划分到一个或多个称为热区的物理区域。 传感器设备跟踪每个热区的温度。 当热区启动过热时，操作系统可以采取措施来冷却区域中的设备。 这些操作可以分为被动冷却或主动冷却。

### <a name="thermal-management-in-windows"></a>Windows 中的热管理

Windows 热量管理模型基于 ACPI 的热区概念。 这是一个合作固件/OS/驱动程序模型，可通过定义完善的接口，从中央热量管理组件抽象传感器和冷却设备。 有关热量管理的详细信息，请参阅[Microsoft Connect 网站](https://aka.ms/connect-redirect?DownloadID=48106)上的标题为 "Windows 中的热量管理" 的文档。

### <a name="acpi-thermal-zones"></a>ACPI 热量区域

热量区域定义为包括执行以下操作的子对象：

-   识别热区中包含的设备：

    -   \_TZD，列出热区中的非处理器设备。
    -   \_PSL，列出热区中的处理器。
-   指定必须采取措施的温度阈值：

    -   \_PSV 以指示操作系统启动被动冷却控制的温度。
    -   \_热以指示操作系统休眠的温度。
    -   \_CRT 以指示操作系统关闭的温度。
-   描述热区的被动冷却行为：

    -   \_OGC-RX-TC1，\_TC2 进行热响应。
    -   \_TSP 获取热区被动冷却的适当温度采样间隔。
-   报告温度区温度：

    -   \_TMP 用于固件报告温度，或
    -   \_HID 和 \_CRS 加载温度传感器驱动程序并向其分配硬件资源。
-   还可以接收其他温度阈值跨越的通知：

    -   \_NTT，用于指定要接收通知的其他阈值交叉。
    -   \_DTI，用于接收附加阈值跨越的通知。
-   （可选）描述热区的活动冷却行为：

    -   \_AL*x*来列出热区中的风扇。
    -   \_AC*x*必须开启风扇*x*的温度。

有关 ACPI 热量区域的详细信息，请参阅[ACPI 5.0 规范](https://uefi.org/specifications)中的第11章 "热量管理"。

### <a name="logical-processor-idling-as-a-thermal-mitigation"></a>作为热缓解的逻辑处理器置于空闲状态

该平台可以向操作系统指示热区中的处理器核心应该空闲（而不是受到限制）。 这是通过在一个或多个热量区域中包含处理器聚合器设备（ACPI000C）来实现的。 超过热量区域的 \_PSV 时，Windows 将停止一些核心。 该数字为 *（1-&lt;zone 被动限制&gt;） \* &lt;热区中的内核数&gt;* 或 \_用途中报告的内核数，以较大者为准。 有关详细信息，请参阅[ACPI 5.0 规范](https://uefi.org/specifications)中的 8.5.1 "逻辑处理器置于空闲状态" 部分。

Oem 可以包含特定于设备的方法（\_DSM）来支持适用于 Windows 的 Microsoft 热量扩展。 有关详细信息，请参阅[Microsoft 热量扩展的特定于设备的方法](device-specific-method-for-microsoft-thermal-extensions.md)。

 

 




