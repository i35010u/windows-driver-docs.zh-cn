---
title: 支持在集成的显示器的亮度控件
description: 支持在集成的显示器的亮度控件
ms.assetid: d32ee274-569e-4adc-a723-28dc756fb177
keywords:
- WDK 显示亮度
- 基于 ACPI 亮度热键 WDK 显示
- 通知 WDK 显示亮度热键
- BIOS 亮度控制 WDK 显示
- 自动亮度 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0aaa29e791956762959ca0567e4eaabbfccf7f03
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526110"
---
# <a name="supporting-brightness-controls-on-integrated-display-panels"></a>支持在集成的显示器的亮度控件


亮度控件中的监视器驱动程序，Monitor.sys，由操作系统提供实现。 监视器驱动程序实现以允许应用程序 （例如操作系统的亮度滑块） 的亮度级别进行交互的 Windows Management Instrumentation (WMI) 接口。 监视器驱动程序注册与设备电源策略引擎 (DPPE)，以便亮度级别响应电源策略中的更改。 使用高级配置和电源接口 (ACPI) 来处理基于 ACPI 亮度键盘快捷方式注册监视器驱动程序。 与的兼容性[Windows 2000 显示器驱动程序模型](windows-2000-display-driver-model-design-guide.md)，显示器驱动程序实现基于 IOCTL 的亮度控件。

显示微型端口驱动程序或由基本输入/输出系统 (BIOS) 可以支持更改集成的显示面板的亮度系统公开的 ACPI 方法。 对于标记为具有输出技术，用于在内部连接的计算机中的第一个视频目标 ([**D3DKMDT\_VOT\_内部**](https://msdn.microsoft.com/library/windows/hardware/ff546605))，监视器驱动程序调用显示微型端口驱动程序[ **DxgkDdiQueryInterface** ](https://msdn.microsoft.com/library/windows/hardware/ff559764)查询函数[亮度控制接口](https://msdn.microsoft.com/library/windows/hardware/ff538260)GUID标识\_DEVINTERFACE\_亮度\_2 和 DXGK\_亮度\_接口\_版本\_1，和[亮度控制接口 V。2 （自适应和平滑的亮度控制）](https://msdn.microsoft.com/library/windows/hardware/jj647485)由 GUID 标识\_DEVINTERFACE\_亮度和 DXGK\_亮度\_接口\_版本\_2。 监视器驱动程序显示微型端口驱动程序不支持至少亮度控制接口，如果查询使用 ACPI \_BCL \_BCM，和\_BQC 子设备上的方法。 有关这些方法的详细信息，请参阅 ACPI 规范上[ACPI 网站](https://go.microsoft.com/fwlink/p/?linkid=57185)。

**请注意**  中 Windows 显示驱动程序模型 (WDDM)，ACPI 标识符不用于识别身份集成的显示面板。 这与不同[Windows 2000 显示器驱动程序模型](windows-2000-display-driver-model-design-guide.md)，它也支持仅显示具有 0x0110 标识符面板。

 

如果显示微型端口驱动程序或 BIOS 公开 ACPI 方法支持亮度控件，显示器驱动程序将注册的亮度键盘快捷方式的 ACPI 通知。 没有备用机制存在是为了指示有关快捷关键通知监视器驱动程序。 如果监视器驱动程序不能使用任一亮度控制机制或显示微型端口驱动程序提供[亮度控制接口](https://msdn.microsoft.com/library/windows/hardware/ff538260)调用将失败，但[ **DxgkDdiGetPossibleBrightness** ](https://msdn.microsoft.com/library/windows/hardware/ff559661)函数，该监视器驱动程序不支持亮度控件。

### <a name="span-idbrightnesslevelsspanspan-idbrightnesslevelsspanspan-idbrightnesslevelsspanbrightness-levels"></a><span id="Brightness_Levels"></span><span id="brightness_levels"></span><span id="BRIGHTNESS_LEVELS"></span>亮度级别

亮度级别从 0 到 100 其中零处于关闭状态，100 是便携式计算机支持的最大亮度表示为范围内的单字节值。 便携式计算机的每台计算机必须报告为 100; 最大亮度级别但是，便携式计算机不需要支持级别为零。 从 0 到 100 的值的唯一要求是更大的值必须代表较高的亮度级别。 级别之间的增量不需要是一致的且便携式计算机可以支持任意数量的最大 101 级别的非重复值。 您必须决定如何将硬件级别映射到的亮度级别值的范围。 但是，显示微型端口驱动程序调用[ **DxgkDdiGetPossibleBrightness** ](https://msdn.microsoft.com/library/windows/hardware/ff559661)函数不应报告更多的亮度级别值比硬件支持。

### <a name="span-iddisablingautomaticbrightnesschangesbythebiosspanspan-iddisablingautomaticbrightnesschangesbythebiosspanspan-iddisablingautomaticbrightnesschangesbythebiosspandisabling-automatic-brightness-changes-by-the-bios"></a><span id="Disabling_Automatic_Brightness_Changes_by_the_BIOS"></span><span id="disabling_automatic_brightness_changes_by_the_bios"></span><span id="DISABLING_AUTOMATIC_BRIGHTNESS_CHANGES_BY_THE_BIOS"></span>禁用自动亮度更改 BIOS

若要避免出现问题，如果系统 BIOS 和监视器驱动程序同时控制显示面板亮度可能会出现，显示微型端口驱动程序应设置 2 位的自变量到\_DOS 方法。 有关详细信息\_DOS 方法和其参数，请参阅 ACPI 规范。 设置位 2，在系统 BIOS 将得到通知，它应执行任何自动亮度更改。

### <a name="span-idbiosrequirementstosupportbrightnesscontrolsspanspan-idbiosrequirementstosupportbrightnesscontrolsspanspan-idbiosrequirementstosupportbrightnesscontrolsspanbios-requirements-to-support-brightness-controls"></a><span id="BIOS_Requirements_to_Support_Brightness_Controls"></span><span id="bios_requirements_to_support_brightness_controls"></span><span id="BIOS_REQUIREMENTS_TO_SUPPORT_BRIGHTNESS_CONTROLS"></span>支持亮度控件的 BIOS 要求

对于显示微型端口驱动程序支持以最佳方式控制集成的面板亮度，请在系统 BIOS 必须提供通过 ACPI 以下各项：

-   亮度控制方法

    集成的面板设备应支持 ACPI 亮度控制方法 (\_BCL \_BCM，和\_BQC)。 \_BCL 和\_BCM 自版本 1.0 b 的 ACPI 规范保持不变; 可以在部分 B.6.2 和 B.6.3 ACPI 3.0 规范中找到它们的定义。 \_BQC 是可选的在部分 B.6.4 ACPI 3.0 规范中定义。 亮度级别定义，请参阅亮度级别。

    以下是 Dispmprt.h 中定义的 ACPI 亮度控制方法的别名：

    -   ACPI\_方法\_输出\_BCLÂ-允许 Windows 查询显示输出设备所支持的亮度级别的列表。 如果集成的 LCD 存在且支持亮度级别，则需要使用此方法。
    -   ACPI\_方法\_输出\_BCMÂ-允许 Windows 将显示输出设备的亮度级别。 Windows 仅在设置级别报告的 ACPI\_方法\_输出\_BCL 方法。 ACPI\_方法\_输出\_BCM 方法是必需的如果 ACPI\_方法\_输出\_BCL 方法的实现。
-   禁用自动系统 BIOS 的亮度控制

    系统 BIOS 应该支持设置位 2 的自变量到\_DOS 方法以允许自动系统 BIOS 亮度更改要禁用在图形适配器上的。 此位是对以前定义的值在此方法中的位的补充。 有关此位的详细信息，请参阅部分 B.4.1 ACPI 3.0 规范中。 如果不支持此位，监视器驱动程序和系统 BIOS 可以更改的亮度级别，这会导致亮度的闪烁，并可能会使亮度设置为一个值，不是用户请求的内容。

    Dispmprt.h 中定义的 ACPI 自动亮度控制方法的以下别名：

    -   ACPI\_方法\_显示\_DOSÂ-指示系统 BIOS 能否自动切换活动显示输出或控制的 LCD 亮度。 允许的参数如下：
        -   ACPI\_ARG\_启用\_自动\_LCD\_亮度。 状态系统 BIOS 在到 DC 从 AC 电源更改时，应自动控制 LCD 的亮度级别。
        -   ACPI\_ARG\_禁用\_自动\_LCD\_亮度。 状态到 DC 从 AC 电源更改时，系统 BIOS 应自动控制 LCD 的亮度级别。
-   亮度键盘快捷方式的通知

    亮度快捷关键通知应定向到集成的显示器面板设备，不适用于图形适配器。

    Dispmprt.h 中定义支持以下通知：

    -   ACPI\_通知\_周期\_亮度\_热键-用户已按热键，对于循环显示亮度。
    -   ACPI\_通知\_INC\_亮度\_热键-用户已按热键，增加显示亮度。
    -   ACPI\_通知\_DEC\_亮度\_热键-用户已按热键，为降低显示亮度。
    -   ACPI\_通知\_零\_亮度\_热键-用户已按热键，减少为零的显示器亮度。

    这些快捷方式的关键通知不熟悉 ACPI 3.0 规范和 B.7 部分所述。 通常情况下，便携式计算机将不支持所有这些快捷方式的重要通知。

    ACPI 监视器驱动程序的默认行为\_通知\_INC\_亮度\_热键和 ACPI\_通知\_DEC\_亮度\_热键通知是递增 （或减少） 亮度至少 5%的 （或更少） 比以前的亮度级别，直到达到下一步提供 5%步骤级别 (5、 10、 15、...、 95，100)。 递增或递减的键盘快捷方式可以创建非对称模式亮度级别，如以下示例所示。

    -   可用\_BCL 亮度控制级别指定为 0、 1、 5、 10、...、 95 中，100

        <span id="Results_using_the_ACPI_NOTIFY_INC_BRIGHTNESS_HOTKEY_notification_"></span><span id="results_using_the_acpi_notify_inc_brightness_hotkey_notification_"></span><span id="RESULTS_USING_THE_ACPI_NOTIFY_INC_BRIGHTNESS_HOTKEY_NOTIFICATION_"></span>结果使用 ACPI\_通知\_INC\_亮度\_热键通知：  
        0, 5, 10, 15, 20, 25, 30, 35, 40, 45, 50, 55, 60, 65, 70, 75, 80, 85, 90, 95, 100

        <span id="Results_using_the_ACPI_NOTIFY_DEC_BRIGHTNESS_HOTKEY_notification_"></span><span id="results_using_the_acpi_notify_dec_brightness_hotkey_notification_"></span><span id="RESULTS_USING_THE_ACPI_NOTIFY_DEC_BRIGHTNESS_HOTKEY_NOTIFICATION_"></span>结果使用 ACPI\_通知\_DEC\_亮度\_热键通知：  
        100, 95, 90, 85, 80, 75, 70, 65, 60, 55, 50, 45, 40, 35, 30, 25, 20, 15, 10, 5, 0

    -   可用\_BCL 亮度控制级别指定为 1、 5、 10、...、 95 中，100

        <span id="Results_using_the_ACPI_NOTIFY_INC_BRIGHTNESS_HOTKEY_notification_"></span><span id="results_using_the_acpi_notify_inc_brightness_hotkey_notification_"></span><span id="RESULTS_USING_THE_ACPI_NOTIFY_INC_BRIGHTNESS_HOTKEY_NOTIFICATION_"></span>结果使用 ACPI\_通知\_INC\_亮度\_热键通知：  
        1, 10, 15, 20, 25, 30, 35, 40, 45, 50, 55, 60, 65, 70, 75, 80, 85, 90, 95, 100

        <span id="Results_using_the_ACPI_NOTIFY_DEC_BRIGHTNESS_HOTKEY_notification_"></span><span id="results_using_the_acpi_notify_dec_brightness_hotkey_notification_"></span><span id="RESULTS_USING_THE_ACPI_NOTIFY_DEC_BRIGHTNESS_HOTKEY_NOTIFICATION_"></span>结果使用 ACPI\_通知\_DEC\_亮度\_热键通知：  
        100, 95, 90, 85, 80, 75, 70, 65, 60, 55, 50, 45, 40, 35, 30, 25, 20, 15, 10, 5, 1

    在后一种示例中，1 是最后一个可用值，因此，该驱动程序为 1 设置的亮度级别，即使它是不超过 5 个百分比单位不同于以前的值为 5。

    通过将 DWORD 值更改，可以重写此默认监视器驱动程序行为。 **MinimumStepPercentage**以下注册表项中：

    `HKEY_LOCAL_MACHINE\ SYSTEM\ CurrentControlSet\ Services\` *监视器*`\ Parameters\`

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关的主题


[支持显示输出和 ACPI 事件](supporting-display-output.md)

 

 






