---
title: WDF 驱动程序选项卡
description: 本主题提供了 WDF 验证程序 WDF 驱动程序页的详细的信息。
ms.assetid: e1e1d92e-1173-48ef-b985-688ebfb08bdc
keywords:
- WDF 验证程序控件应用程序 WDK
- WDF 验证程序 WDK
- 工具 WDK，验证
- 测试驱动程序 WDK WDF
- 调试驱动程序 WDK WDF
- 验证驱动程序 WDK WDF
- KMDF 验证程序工具 WDK WDF
- UMDF 验证程序工具 WDK WDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 42d5dc32f07ef053034be198bf87154ab0de632a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380465"
---
# <a name="wdf-drivers-tab"></a>WDF 驱动程序选项卡


本主题提供有关 WDF 验证程序的详细的信息**WDF 驱动程序**页。 此页面列出了所有 WDF 驱动程序的计算机上，并且可以更改其验证设置和使用它们的设备的设置。 如果您感兴趣的特定驱动程序下，从这里开始。

在启动应用程序时，将在系统上当前看到 WDF 驱动程序和运行时版本的列表。 每个行包含的驱动程序二进制文件、 其服务显示名称、 框架版本中，名称和 KMDF 驱动程序，请启动类型。

当您突出显示驱动程序时，您将看到当前正在使用该驱动程序，任何设备以及相关 UMDF 主机进程。 选择正在运行的 UMDF 驱动程序时，宿主进程控件才可见。

![方 wdf 驱动程序选项卡的屏幕截图](images/wdfverifier-tab1.png)

## <a name="span-idcolorschemespanspan-idcolorschemespanspan-idcolorschemespancolor-scheme"></a><span id="Color_Scheme"></span><span id="color_scheme"></span><span id="COLOR_SCHEME"></span>配色方案


对于每个驱动程序，具有颜色编码的图标指示它使用 KMDF、 UMDF 1 或 UMDF 2。

颜色代码指示驱动程序的状态和需要执行，以便对驱动程序的验证设置的更改生效。

-   蓝色表示驱动程序正在使用中并且与一个或多个即插即用设备相关联。 对于以使更改生效，您需要禁用和重新启用这些设备。 你可以选择是否 WDF 验证程序执行此上**我的首选项**选项卡。这些驱动程序，请您获取关联的设备的列表。
-   红色表示驱动程序是在使用中，但并不与即插即用设备相关联。 有关以使更改生效：
    -   对于 KMDF，您必须重新启动。
    -   对于 UMDF，必须停止并重新启动所有 UMDF 宿主进程。
-   绿色表示驱动程序当前未使用。 如果您更改设置，所做的更改生效的下次加载了驱动程序。

## <a name="span-idpresetoptionsspanspan-idpresetoptionsspanspan-idpresetoptionsspanpreset-options"></a><span id="Preset_Options"></span><span id="preset_options"></span><span id="PRESET_OPTIONS"></span>预设的选项


具有特定于驱动程序的设置 （KMDF 和 UMDF 2） 的驱动程序，请右键单击以下快速选项菜单的驱动程序名称：

-   设置为默认设置。
-   启用 WDF 断点和驱动程序代码中的验证宏。
-   启用所有建议进行的测试设置 （上详细和更大 IFR 缓冲区，下层验证验证程序）。

如果更改驱动程序的设置，但尚未提交所做的更改，(\*) 驱动程序名称之后出现的菜单包含其他选项以撤消更改和。

## <a name="span-idchangingindividualverificationsettingsforadriverspanspan-idchangingindividualverificationsettingsforadriverspanspan-idchangingindividualverificationsettingsforadriverspanchanging-individual-verification-settings-for-a-driver"></a><span id="Changing_Individual_Verification_Settings_for_a_Driver"></span><span id="changing_individual_verification_settings_for_a_driver"></span><span id="CHANGING_INDIVIDUAL_VERIFICATION_SETTINGS_FOR_A_DRIVER"></span>更改驱动程序的单独的验证设置


单击 + 左侧的颜色图标以查看驱动程序的当前验证设置。 您可以右键单击各个选项来更改它们。

右键单击一个布尔设置切换它。 其他人演示一个编辑控件可以在其中键入值时，某些设置存在有效选项的列表。 如果输入值无效时发出提示音应用程序。 按**Enter**使用你的新值或单击要取消更改的控件外部。

必须输入中的十六进制值**AllocateFailCount**，和的一个十进制值**HostTimeoutSeconds**。

如果启用，需要 KMDF 验证程序的功能和**VerifierOn**选项是当前关机，应用程序打开它。 您仍然可以禁用它手动。 在这种情况下，描述该功能的文本指示它将执行的操作如果验证程序上。 在文本描述可以看到设置的状态，只要设置类似的更改取决于其他设置或应用程序验证程序或驱动程序验证程序的使用情况。

如果启动和停止设备或安装新的驱动程序，则必须重新启动 WDF 验证程序来更新清单。

如果在上进行更改**WDF 驱动程序**页上，你会看到上反映这些变化**使用 WDF 设备**页。

 

 





