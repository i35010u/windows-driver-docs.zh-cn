---
title: ACPI 定义的设备
description: ACPI 5.0 规范定义了多个设备类型来代表和控制典型平台功能。
ms.assetid: 10BD17C9-E8FE-41E0-BD8C-E622B60E6BB6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5be0e0a433a2dc6346e5f29d7e1dd8643e62cdab
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56520556"
---
# <a name="acpi-defined-devices"></a>ACPI 定义的设备


[ACPI 5.0 规范](https://www.uefi.org/specifications)定义多个设备类型来代表和控制典型平台功能。 例如，ACPI 定义电源按钮、 睡眠按钮和系统指标。 对于基于 SoC 的平台，Windows 提供了内置驱动程序以支持在本文中所述的 ACPI 定义设备。

有关详细信息，请参阅 ACPI 5.0 规范的第 9，"ACPI-Defined 设备和特定于设备的对象"部分。

## <a href="" id="lid"></a>合上盖子设备


此设备描述，并报告状态的蛤设备的合上盖子。 详细信息，请参阅部分 9.4，"控制方法合上盖子设备"中[ACPI 5.0 规范](https://www.uefi.org/specifications)。 合上盖子设备实现使用 GPIO 信号 ACPI 事件机制，在 ACPI 5.0 规范 5.6.5，"GPIO-Signaled ACPI 事件"部分中所述。

## <a href="" id="battery"></a>控制方法电池设备


此设备描述、 配置和报告平台电池的状态。 详细信息，请参阅 10.2，"控制方法电池"一节中[ACPI 5.0 规范](https://www.uefi.org/specifications)。 在 SoC 平台上的控制方法电池实现使用 GPIO 信号 ACPI 事件机制，在 ACPI 5.0 规范 5.6.5，"GPIO-Signaled ACPI 事件"部分中所述。 对电池和充电硬件的访问是通过运行通过 GPIO 或存储 OpRegions，5.5.2.4.4 和 5.5.2.4.5 ACPI 5.0 规范的各节所述的方法。

有关在 Windows 中的电池管理的详细信息，请参阅[Windows 功能和电池子系统要求](https://msdn.microsoft.com/library/windows/hardware/mt614876)。

**电池特定于设备的方法 (\_DSM)**

若要支持电池的被动热量管理平台，Microsoft 定义\_DSM 方法进行通信平台固件散热限制限制由电池的散热区域设置。 有关详细信息，请参阅以下文章：

-   [电池特定于设备的方法](battery-device-specific-method.md)
-   [热感区域](#thermal)

## <a href="" id="time"></a>控制方法的时间和警报的设备


ACPI 5.0 定义的操作和可选控制基于方法的时间和警报设备，从而提供了独立于硬件的抽象和更可靠的替代项为实时时钟 (RTC) 的定义。 有关详细信息，请参阅部分 9.15，"PC / AT RTC/CMOS 设备"，和在部分 9.18，"时间和警报设置"， [ACPI 5.0 规范](https://www.uefi.org/specifications)。 如果的标准 PC RTC 未实现或用作备份的时间和警报的设备，FADT 的引导体系结构的"CMOS RTC 不存在"位 RTC 硬件标志必须设置字段。

时间和警报的设备的时间功能所需的支持 InstantGo 功能 （和连接待机电源模式） 的平台。 这些功能在系统电源转换中保持的时间信息，并跟踪的时间甚至时在平台处于关闭状态。 应在平台上的时间将一致时使用不同的固件接口来查询平台时间。 例如，以获得时间的 UEFI 调用应返回操作系统所获取的使用时间和警报设备的相同时间。

必须为 UEFI 时服务的同一时间源从驱动的时间和警报的设备。

## <a href="" id="thermal"></a>热感区域


若要支持 ACPI 热量管理，系统设计器会将一种硬件平台以逻辑方式分区到一个或多个称为热区域的物理区域。 传感器设备跟踪每个热量区域中的温度。 在热区域开始过热，操作系统可以采取措施以冷却区域中的设备。 这些操作可以划分为被动冷却或活动冷却。

### <a name="thermal-management-in-windows"></a>在 Windows 中的散热

Windows 热量管理模型基于 ACPI 的热量区域概念。 这是一个协作的固件/OS/驱动程序模型，用于提取的传感器和冷却设备从中心热量管理组件通过定义完善的接口。 热量管理有关的详细信息，请参阅上标题为"在 Windows 的热量管理"的文档[Microsoft Connect 网站](http://connect.microsoft.com/site1304/Downloads/DownloadDetails.aspx?DownloadID=48106)。

### <a name="acpi-thermal-zones"></a>ACPI 热量区域

热感区域定义以包括子对象，请执行下列操作：

-   确定该热量区域中包含的设备：

    -   \_若要列出散热区域中的非处理器设备 TZD。
    -   \_若要列出散热区域中的处理器的 PSL。
-   指定必须在其中执行操作的温度阈值：

    -   \_PSV 以指示操作系统开始被动冷却的控件的温度。
    -   \_热，以指示操作系统使休眠的温度。
    -   \_CRT 以指示操作系统下，关闭的温度。
-   介绍了过热区域的被动冷却行为：

    -   \_TC1， \_TC2 的热量响应能力。
    -   \_被动冷却的散热区域的相应温度采样间隔的 TSP。
-   报告过热区域的温度：

    -   \_TMP 固件报告温度或
    -   \_HID 和\_CRS 用于加载温度传感器驱动程序和硬件资源分配到它。
-   （可选） 接收通知的跨越其他温度阈值：

    -   \_若要接收的通知用于指定其他阈值交点 NTT。
    -   \_用于接收通知的其他阈值交点 DTI。
-   （可选） 描述热量区域的活动的冷却行为：

    -   \_AL*x*用于列出散热区域中的风扇。
    -   \_AC*x*在哪个风扇温度*x*必须开启。

有关 ACPI 热量区域的详细信息，请参阅"热量管理"，第 11 章中[ACPI 5.0 规范](https://www.uefi.org/specifications)。

### <a name="logical-processor-idling-as-a-thermal-mitigation"></a>热感缓解空闲的逻辑处理器

该平台可以指示给系统散热区域中的处理器核心应为空闲状态 （而不是受到限制）。 这是通过包括处理器聚合器设备 (ACPI000C) 在一个或多个热区域。 Windows 将驻留的大量核心时散热区域\_PSV 跨越。 号 *(1-&lt;区域被动限制&gt;) \* &lt;散热区域中的内核数&gt;*，或报告中的内核数\_用途，两者中较大。 详细信息，请参阅部分 8.5.1，"逻辑处理器空闲"，在[ACPI 5.0 规范](https://www.uefi.org/specifications)。

Oem 可以包括特定于设备的方法 (\_DSM) 以支持 Microsoft 热量扩展的 Windows。 有关详细信息，请参阅[热量的 Microsoft 扩展的特定于设备的方法](device-specific-method-for-microsoft-thermal-extensions.md)。

 

 




