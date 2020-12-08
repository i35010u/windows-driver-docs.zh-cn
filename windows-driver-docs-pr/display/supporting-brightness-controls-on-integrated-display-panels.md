---
title: 在集成显示面板上支持亮度控件
description: 在集成显示面板上支持亮度控件
keywords:
- 亮度 WDK 显示
- 基于 ACPI 的亮度热键显示屏
- 通知亮度热键热键显示
- BIOS 亮度控制 WDK 显示
- 自动显示亮度 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b89ee89b189b583cdd4512cafff0e58b7b7af6e6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96818587"
---
# <a name="supporting-brightness-controls-on-integrated-display-panels"></a>在集成显示面板上支持亮度控件


亮度控制在操作系统提供的监视驱动程序 Monitor.sys 中实现。 监视驱动程序实现 Windows Management Instrumentation (WMI) 接口，以允许应用程序 (例如操作系统的亮度滑块) 以与亮度级别交互。 监视驱动程序将向设备电源策略引擎注册 (DPPE) ，以便亮度级别对电源策略中的更改做出响应。 监视驱动程序将向高级配置和电源接口注册 (ACPI) 来处理基于 ACPI 的亮度快捷键。 为了与 [Windows 2000 显示器驱动程序模型](windows-2000-display-driver-model-design-guide.md)兼容，监视驱动程序实现了基于 IOCTL 的亮度控件。

系统基本输入/输出系统公开的显示微型端口驱动程序或 ACPI 方法 (BIOS) 可以支持更改集成显示面板的亮度。 对于标记为具有在计算机内部连接的输出技术的第一个视频目标 ([**D3DKMDT \_ VOT \_ INTERNAL**](/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_d3dkmdt_video_output_technology)) ，监视驱动程序调用显示微型端口驱动程序的 [**DXGKDDIQUERYINTERFACE**](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_query_interface)函数来查询由 guid DEVINTERFACE [Brightness Control Interface](/windows-hardware/drivers/ddi/index) \_ \_ 亮度 \_ 2 和 DXGK 亮度接口版本1标识的亮度控制接口 \_ \_ \_ \_ ，并使用 [亮度控制接口 (自适应和平滑亮度控制)](/windows-hardware/drivers/ddi/index)由 GUID \_ DEVINTERFACE \_ 亮度和 DXGK \_ 亮度 \_ 接口 \_ 版本 \_ 2 标识。 如果显示微型端口驱动程序不支持至少亮度控制接口，则监视驱动程序将使用 ACPI \_ \_ 在子设备上查询 BCL、BCM 和 \_ BQC 方法。 有关这些方法的详细信息，请参阅 [acpi 网站](https://go.microsoft.com/fwlink/p/?linkid=57185)上的 acpi 规范。

**注意**   在 Windows 显示器驱动程序模型 (WDDM) 中，不使用 ACPI 标识符标识集成的显示面板。 这不同于 [Windows 2000 显示器驱动程序模型](windows-2000-display-driver-model-design-guide.md)，后者仅支持标识符为0x0110 的显示面板。

 

如果显示微型端口驱动程序或 BIOS 公开的 ACPI 方法支持亮度控件，则监视驱动程序将注册亮度快捷键的 ACPI 通知。 不存在用于向监视器驱动程序指示快捷键通知的备用机制。 如果监视器驱动程序无法使用亮度控制机制，或者显示微型端口驱动程序提供 [亮度控制接口](/windows-hardware/drivers/ddi/index) ，但未能调用 [**DxgkDdiGetPossibleBrightness**](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgk_brightness_get_possible) 函数，则监视器驱动程序不支持亮度控件。

### <a name="span-idbrightness_levelsspanspan-idbrightness_levelsspanspan-idbrightness_levelsspanbrightness-levels"></a><span id="Brightness_Levels"></span><span id="brightness_levels"></span><span id="BRIGHTNESS_LEVELS"></span>亮度级别

亮度级别以单字节值的形式表示，范围为0到100，其中0表示关闭，100表示便携式计算机支持的最大亮度。 每台便携式计算机必须报告最大亮度级别 100;但是，便携式计算机不需要支持零级别。 从零到100的值的唯一要求是，较大的值必须表示较高的亮度级别。 级别之间的增量不需要一致，便携式计算机可以支持任意数量的非重复值，最多可达101级别。 必须决定如何将硬件级别映射到亮度级别值的范围。 但是，对显示微型端口驱动程序的 [**DxgkDdiGetPossibleBrightness**](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgk_brightness_get_possible) 函数的调用不应报告比硬件支持的更多的亮度级别值。

### <a name="span-iddisabling_automatic_brightness_changes_by_the_biosspanspan-iddisabling_automatic_brightness_changes_by_the_biosspanspan-iddisabling_automatic_brightness_changes_by_the_biosspandisabling-automatic-brightness-changes-by-the-bios"></a><span id="Disabling_Automatic_Brightness_Changes_by_the_BIOS"></span><span id="disabling_automatic_brightness_changes_by_the_bios"></span><span id="DISABLING_AUTOMATIC_BRIGHTNESS_CHANGES_BY_THE_BIOS"></span>禁用 BIOS 自动亮度更改

若要避免系统 BIOS 和监视器驱动程序都控制显示面板亮度时可能发生的问题，则显示微型端口驱动程序应将参数的第2位设置为 \_ DOS 方法。 有关 \_ DOS 方法及其参数的详细信息，请参阅 ACPI 规范。 通过设置第2位，系统 BIOS 会得到通知，不应执行任何自动亮度更改。

### <a name="span-idbios_requirements_to_support_brightness_controlsspanspan-idbios_requirements_to_support_brightness_controlsspanspan-idbios_requirements_to_support_brightness_controlsspanbios-requirements-to-support-brightness-controls"></a><span id="BIOS_Requirements_to_Support_Brightness_Controls"></span><span id="bios_requirements_to_support_brightness_controls"></span><span id="BIOS_REQUIREMENTS_TO_SUPPORT_BRIGHTNESS_CONTROLS"></span>支持亮度控件的 BIOS 要求

为了使显示微型端口驱动程序支持以最佳方式控制集成面板亮度，系统 BIOS 必须通过 ACPI 提供以下各项：

-   亮度控制方法

    集成面板设备应支持 (\_ BCL、 \_ BCM 和 BQC) 的 ACPI 亮度控制方法 \_ 。 \_\_由于 acpi 规范的1.0 版 B，BCL 和 BCM 不变; 你可以在3.0 部分的 acpi 规范中找到其定义。 \_BQC 是可选的，在第3.0 节的 ACPI 规范中进行了定义。 有关亮度级别的定义，请参阅亮度级别。

    下面是在 Dispmprt 中定义的 ACPI 亮度控制方法的别名：

    -   ACPI \_ 方法 \_ 输出 \_ BCLÂ-允许 Windows 查询显示输出设备支持的一系列亮度级别。 如果集成 LCD 存在并且支持亮度级别，则此方法是必需的。
    -   ACPI \_ 方法 \_ 输出 \_ BCMÂ-允许 Windows 设置显示输出设备的亮度级别。 Windows 只会设置由 ACPI \_ 方法 \_ 输出 BCL 方法报告的级别 \_ 。 \_ \_ \_ 如果实现了 acpi \_ 方法 \_ 输出 \_ BCL 方法，则需要 acpi 方法输出 BCM 方法。
-   禁用自动系统 BIOS 亮度控件

    系统 BIOS 应支持将自变量的第二个参数设置为 \_ 图形适配器上的 DOS 方法，以允许禁用自动系统 BIOS 亮度更改。 此位是对此方法中的位的先前定义的值的补充。 有关此方面的详细信息，请参阅 ACPI 3.0 规范中的第4.1 节。 如果此位不受支持，则监视器驱动程序和系统 BIOS 都可以更改亮度级别，这会导致亮度闪烁，并可能会将亮度设置为不是用户请求的值。

    Dispmprt 中定义了 ACPI 自动亮度控制方法的以下别名：

    -   ACPI \_ 方法 \_ 显示 \_ DOSÂ-表示系统 BIOS 能够自动切换活动显示输出或控制 LCD 亮度。 允许使用以下参数：
        -   ACPI \_ ARG \_ 启用 \_ 自动 \_ LCD \_ 亮度。 指出当电源从 AC 更改为 DC 时，系统 BIOS 应自动控制 LCD 的亮度级别。
        -   ACPI \_ ARG \_ 禁用 \_ 自动 \_ LCD \_ 亮度。 指出当电源从 AC 改为直流时，系统 BIOS 不应自动控制 LCD 的亮度级别。
-   亮度快捷键通知

    亮度快捷方式密钥通知应针对集成显示面板设备，而不是图形适配器。

    支持以下通知，如 Dispmprt 中所定义：

    -   ACPI \_ 通知 \_ 循环 \_ 亮度 \_ 热键-用户按了热键来循环显示亮度。
    -   ACPI \_ 通知 \_ Inc. 的 \_ 亮度 \_ 热键-用户已经按了热键增加了显示亮度。
    -   ACPI \_ 通知 \_ DEC \_ 亮度 \_ 热键-用户按下了用于减小显示器亮度的热键。
    -   ACPI \_ 通知 \_ 零 \_ 亮度 \_ 热键-用户已经按了用于将显示亮度降低为零的热键。

    这些快捷键通知是 ACPI 3.0 规范的新手，详见第7部分。 通常，便携式计算机不支持所有这些快捷键通知。

    用于 ACPI \_ 通知 \_ 公司 \_ 亮度 \_ 热键和 acpi 通知 DEC 亮度热键通知的监视驱动程序的默认行为 \_ \_ \_ \_ 是增加 (或) 降低) 亮度比之前亮度级别至少增加 5 (%，直到达到下一个可用的5% 步骤级别 (5，10，15，...，95，100) 。 用快捷键递增或递减可以在亮度级别中创建非对称模式，如以下示例中所示。

    -   可用的 \_ BCL 亮度控制级别指定为0，1，5，10，...，95，100

        <span id="Results_using_the_ACPI_NOTIFY_INC_BRIGHTNESS_HOTKEY_notification_"></span><span id="results_using_the_acpi_notify_inc_brightness_hotkey_notification_"></span><span id="RESULTS_USING_THE_ACPI_NOTIFY_INC_BRIGHTNESS_HOTKEY_NOTIFICATION_"></span>使用 ACPI \_ 通知 \_ Inc. \_ 亮度 \_ 热键通知的结果：  
        0、5、10、15、20、25、30、35、40、45、50、55、60、65、70、75、80、85、90、95、100

        <span id="Results_using_the_ACPI_NOTIFY_DEC_BRIGHTNESS_HOTKEY_notification_"></span><span id="results_using_the_acpi_notify_dec_brightness_hotkey_notification_"></span><span id="RESULTS_USING_THE_ACPI_NOTIFY_DEC_BRIGHTNESS_HOTKEY_NOTIFICATION_"></span>使用 ACPI \_ 通知 \_ DEC \_ 亮度 \_ 热键通知的结果：  
        100，95，90，85，80，75，70，65，60，55，50，45，40，35，30，25，20，15，10，5，0

    -   可用的 \_ BCL 亮度控制级别指定为1、5、10、...、95、100

        <span id="Results_using_the_ACPI_NOTIFY_INC_BRIGHTNESS_HOTKEY_notification_"></span><span id="results_using_the_acpi_notify_inc_brightness_hotkey_notification_"></span><span id="RESULTS_USING_THE_ACPI_NOTIFY_INC_BRIGHTNESS_HOTKEY_NOTIFICATION_"></span>使用 ACPI \_ 通知 \_ Inc. \_ 亮度 \_ 热键通知的结果：  
        1、10、15、20、25、30、35、40、45、50、55、60、65、70、75、80、85、90、95、100

        <span id="Results_using_the_ACPI_NOTIFY_DEC_BRIGHTNESS_HOTKEY_notification_"></span><span id="results_using_the_acpi_notify_dec_brightness_hotkey_notification_"></span><span id="RESULTS_USING_THE_ACPI_NOTIFY_DEC_BRIGHTNESS_HOTKEY_NOTIFICATION_"></span>使用 ACPI \_ 通知 \_ DEC \_ 亮度 \_ 热键通知的结果：  
        100、95、90、85、80、75、70、65、60、55、50、45、40、35、30、25、20、15、10、5、1

    在后一个示例中，1是最后一个可用值，因此驱动程序将亮度级别设置为1，即使它小于之前值5的5% 单位不同。

    通过更改 DWORD 的值，可以重写此默认的监视器驱动程序行为。 以下注册表项中的 **MinimumStepPercentage** ：

    `HKEY_LOCAL_MACHINE\ SYSTEM\ CurrentControlSet\ Services\`*监视器*`\ Parameters\`

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[支持显示输出和 ACPI 事件](supporting-display-output.md)

 

