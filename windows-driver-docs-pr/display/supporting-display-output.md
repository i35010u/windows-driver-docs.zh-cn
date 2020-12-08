---
title: 支持显示输出和 ACPI 事件
description: 系统配置和设备电源控制的综合方法基于 ACPI 规范内置于 Windows 中。
keywords:
- ACPI 显示 WDK 显示
- 基于 ACPI 的显示热键 WDK 显示
- 显示热键 WDK 显示
- BIOS 显示控制 WDK 显示
- 自动显示开关 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bec48aa17c88d3459f3af3f09724ce4ab8f3a540
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96830623"
---
# <a name="supporting-display-output-and-acpi-events"></a>支持显示输出和 ACPI 事件


基于高级配置和电源接口 (ACPI) 规范，在 Windows 中内置了一种全面的系统配置和设备电源控制方法。 Windows 支持驱动程序可以使用的功能来管理显示输出设备的配置和功能。 有关详细信息，请参阅 [acpi 网站](https://go.microsoft.com/fwlink/p/?linkid=57185)上的 acpi 规范。

## <a name="span-idbios_requirements_to_support_display_output_devicesspanspan-idbios_requirements_to_support_display_output_devicesspanspan-idbios_requirements_to_support_display_output_devicesspanbios-requirements-to-support-display-output-devices"></a><span id="BIOS_Requirements_to_Support_Display_Output_Devices"></span><span id="bios_requirements_to_support_display_output_devices"></span><span id="BIOS_REQUIREMENTS_TO_SUPPORT_DISPLAY_OUTPUT_DEVICES"></span>支持显示输出设备的 BIOS 要求


系统 BIOS 公开的显示微型端口驱动程序或 ACPI 方法支持显示输出设备配置。 调用 [**DxgkDdiNotifyAcpiEvent**](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_notify_acpi_event) 函数以通知显示有关 ACPI 事件的显示微型端口驱动程序。 例如，当用户按下输出设备开关的键盘快捷方式时，将调用 **DxgkDdiNotifyAcpiEvent** 函数，其中包含 acpi \_ 通知 \_ 循环 \_ 显示 \_ 热键通知和请求类型 DXGK \_ ACPI \_ 更改 \_ 显示 \_ 模式。 因此，操作系统将调用 [**DxgkDdiRecommendFunctionalVidPn**](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_recommendfunctionalvidpn) 函数来查询选定的显示输出设备。

Dispmprt 中定义了 ACPI 显示输出的以下别名：

-   ACPI \_ 方法 \_ 显示 \_ DOD-枚举附加到显示适配器的所有设备。 如果集成控制器支持切换输出设备，则此方法是必需的。 这是 \_ 由 ACPI 规范定义的 DOD 方法的别名。
-   ACPI \_ 方法 \_ 显示 \_ DOS-表示系统固件能够自动切换活动显示输出。 这是 \_ 由 ACPI 规范定义的 SOD 方法的别名。 允许使用以下参数：
    -   ACPI \_ ARG \_ 启用 \_ SWITCH \_ 事件。 指出系统固件不应自动切换活动显示输出设备。 相反，它必须将所需的更改保存在与每个显示输出设备关联的状态变量中，并生成显示切换事件。 操作系统可以通过调用 ACPI \_ 方法 \_ OUTPUT dg 方法来查询设备的活动状态 \_ 。
    -   ACPI \_ ARG \_ 启用 \_ 自动 \_ 切换。 表明系统固件应自动切换活动显示输出设备，而不与操作系统交互。 它不会生成显示切换事件。
    -   ACPI \_ ARG \_ 禁用 \_ SWITCH \_ 事件。 指出系统固件不应执行任何操作;也就是说，不会切换输出设备，也不会通知操作系统。 ACPI \_ 方法 \_ OUTPUT dg 方法返回的值 \_ 将被锁定。
-   ACPI \_ 方法 \_ 输出 \_ dc-返回显示输出设备的状态。 这是 \_ 由 ACPI 规范定义的 CSD 方法的别名。
-   ACPI \_ 方法 \_ 输出 \_ dg-检查显示输出设备的状态是否处于活动状态。 这是 \_ 由 ACPI 规范定义的 SGD 方法的别名。
-   ACPI \_ 方法 \_ 输出 \_ DSS-将显示输出设备的状态设置为 "活动" 或 "非活动"。 这是 \_ 由 ACPI 规范定义的 SSD 方法的别名。 操作系统管理此操作以避免闪烁。
-   ACPI \_ 方法 \_ 显示 \_ GPD-查询 CMOS 条目，以确定在启动时发送的视频设备。 这是 \_ 由 ACPI 规范定义的 DPG 方法的别名。
-   ACPI \_ 方法 \_ 显示 \_ SPD-更新 CMOS 条目，以确定在启动时发布的视频设备。 这是 \_ 由 ACPI 规范定义的 DPS 方法的别名。
-   ACPI \_ 方法 \_ 显示 \_ VPO-确定实现了哪些视频选项。 这是 \_ 由 ACPI 规范定义的 OPV 方法的别名。

## <a name="span-idexternal_asynchronous_eventsspanspan-idexternal_asynchronous_eventsspanspan-idexternal_asynchronous_eventsspanexternal-asynchronous-events"></a><span id="External_Asynchronous_Events"></span><span id="external_asynchronous_events"></span><span id="EXTERNAL_ASYNCHRONOUS_EVENTS"></span>外部异步事件


必须通知操作系统有关影响显示输出设备的外部异步事件。 以下通知和相关请求类型在 Dispmprt 中定义，并在 [**DxgkDdiNotifyAcpiEvent**](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_notify_acpi_event) 函数中使用。

-   ACPI \_ 通知 \_ 循环 \_ 显示 \_ 热键-通知操作系统用户已按下了循环显示键盘快捷方式。
-   ACPI \_ 通知 \_ 下一个 \_ 显示 \_ 热键-通知操作系统用户已按下了下一个显示键盘快捷方式。
-   ACPI \_ 通知 \_ 上 \_ \_ 一个显示热键-通知操作系统用户已按下了上一个显示键盘快捷方式。

**注意**  上述通知依赖于处理用户在按键盘快捷方式时引发的事件。

 

下面是显示微型端口驱动程序可对操作系统执行的请求类型。

-   DXGK \_ ACPI \_ 更改 \_ 显示 \_ 模式-启动模式的请求更改为新建议的活动视频现有网络 (VidPN) 。
-   DXGK \_ ACPI \_ 轮询 \_ 显示 \_ 孩子-请求轮询显示适配器的子适配器的连接。

**注意** 前面的请求是 [**DxgkDdiNotifyAcpiEvent**](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_notify_acpi_event)函数返回的 *AcpiFlags* 参数的值。

 

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[在集成显示面板上支持亮度控件](supporting-brightness-controls-on-integrated-display-panels.md)

 

