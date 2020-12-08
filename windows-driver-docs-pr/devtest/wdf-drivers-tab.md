---
title: WDF 驱动程序选项卡
description: 本主题提供有关 WDF 验证程序的 WDF 驱动程序页面的详细信息。
keywords:
- WDF 验证器控件应用程序 WDK
- WDF 验证程序 WDK
- 工具 WDK，验证
- 测试驱动程序 WDK WDF
- 调试驱动程序 WDK WDF
- 验证驱动程序 WDK WDF
- KMDF 验证程序工具 WDK WDF
- UMDF 验证程序工具 WDK WDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 052c98758bb7ceb89f6ebe1a6cec3cf51294499a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96823361"
---
# <a name="wdf-drivers-tab"></a>WDF 驱动程序选项卡


本主题提供有关 WDF 验证 **程序的 Wdf 驱动程序** 页面的详细信息。 此页面列出计算机上的所有 WDF 驱动程序，你可以更改其验证设置以及使用这些驱动程序的设备的设置。 如果你对特定驱动程序感兴趣，请从此处开始。

当你启动应用程序时，你将看到当前在系统上的 WDF 驱动程序和运行时版本的列表。 每行都包含驱动程序二进制文件的名称、其服务显示名称、框架版本和 KMDF 驱动程序的启动类型。

突出显示某个驱动程序时，将看到当前正在使用该驱动程序的任何设备，以及相关的 UMDF 主机进程。 仅当选择正在运行的 UMDF 驱动程序时，主机进程控制才可见。

!["wdf 驱动程序" 选项卡的屏幕截图](images/wdfverifier-tab1.png)

## <a name="span-idcolor_schemespanspan-idcolor_schemespanspan-idcolor_schemespancolor-scheme"></a><span id="Color_Scheme"></span><span id="color_scheme"></span><span id="COLOR_SCHEME"></span>配色方案


对于每个驱动程序，使用彩色编码的图标指示它使用的是 KMDF、UMDF 1 还是 UMDF 2。

颜色代码指示驱动程序的状态和需要执行的操作，以便对驱动程序的验证设置的更改生效。

-   蓝色表示驱动程序正在使用中，并与一个或多个 PnP 设备相关联。 要使更改生效，需要禁用并重新启用这些设备。 可以在 " **我的首选项** " 选项卡上选择 WDF 验证程序是否执行此功能。对于这些驱动程序，你将获得相关设备的列表。
-   红色表示驱动程序正在使用中，但它与 PnP 设备无关。 要使更改生效：
    -   对于 KMDF，必须重新启动。
    -   对于 UMDF，必须停止并重新启动所有 UMDF 主机进程。
-   绿色表示当前未使用驱动程序。 如果更改设置，则所做的更改将在下次加载驱动程序时生效。

## <a name="span-idpreset_optionsspanspan-idpreset_optionsspanspan-idpreset_optionsspanpreset-options"></a><span id="Preset_Options"></span><span id="preset_options"></span><span id="PRESET_OPTIONS"></span>预设选项


对于具有特定驱动程序设置 (KMDF 和 UMDF 2) 的驱动程序，请右键单击以下快速选项菜单的驱动程序名称：

-   设置为默认设置。
-   启用 WDF 断点并验证驱动程序代码中的宏。
-   启用 (验证程序上的所有推荐的测试设置、详细和更大的 IFR 缓冲区、下层验证) 。

如果更改驱动程序的设置，但尚未提交更改， (\*) 会出现在驱动程序名称之后，并且该菜单包含一个用于撤消更改的附加选项。

## <a name="span-idchanging_individual_verification_settings_for_a_driverspanspan-idchanging_individual_verification_settings_for_a_driverspanspan-idchanging_individual_verification_settings_for_a_driverspanchanging-individual-verification-settings-for-a-driver"></a><span id="Changing_Individual_Verification_Settings_for_a_Driver"></span><span id="changing_individual_verification_settings_for_a_driver"></span><span id="CHANGING_INDIVIDUAL_VERIFICATION_SETTINGS_FOR_A_DRIVER"></span>更改驱动程序的单独验证设置


单击 "颜色" 图标左侧的 "+" 以查看驱动程序的当前验证设置。 可以右键单击各个选项进行更改。

右键单击布尔值设置将对其进行切换。 某些设置显示有效选项的列表，而其他设置则显示 "编辑" 控件，你可以在其中键入值。 如果输入的值无效，应用会发出嘟嘟声。 按 **enter** 以使用新值，或在控件外部单击以取消更改。

必须在 **AllocateFailCount** 中输入十六进制值，并在 **HostTimeoutSeconds** 中输入一个十进制值。

如果启用需要 KMDF 的验证程序的功能，并且 **VerifierOn** 选项目前处于关闭状态，则应用程序将其打开。 你仍可手动禁用它。 在这种情况下，描述该功能的文本表明了在验证程序打开时该如何操作。 每当设置依赖于其他设置，或使用应用程序验证程序或驱动程序验证程序时，都会出现说明设置状态的文本中的类似更改。

如果启动和停止设备或安装新的驱动程序，则必须重新启动 WDF 验证程序以更新清单。

如果在 " **Wdf 驱动程序** " 页上进行了更改，则会看到这些更改反映在 " **使用 WDF 的设备** " 页上。

 

 





