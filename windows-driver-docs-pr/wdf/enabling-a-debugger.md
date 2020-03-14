---
title: 如何启用对 UMDF 驱动程序的调试
description: 如何启用对 UMDF 驱动程序的调试
ms.assetid: ea37eb7b-09fa-4c8d-aff7-273b07bc0007
keywords:
- 调试器 WDK UMDF
- 调试器 WDK UMDF，启用
- 用户模式驱动程序框架 WDK，启用调试器
- UMDF WDK，启用调试器
- 用户模式驱动程序 WDK UMDF，启用调试器
- 调试驱动程序 WDK UMDF，启用调试器
- 驱动程序调试 WDK UMDF，启用调试器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: afaf1f6e452ecbf784907f87842f6ee64b2e0aac
ms.sourcegitcommit: b316c97bafade8b76d5d3c30d48496915709a9df
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/13/2020
ms.locfileid: "79242888"
---
# <a name="how-to-enable-debugging-of-a-umdf-driver"></a>如何启用对 UMDF 驱动程序的调试


你可以使用以下配置来调试用户模式驱动程序框架（UMDF）驱动程序。 所有配置都涉及两台计算机，即主机和目标。 运行 Microsoft Visual Studio 和 Windows 驱动程序工具包（WDK）来构建主机上的驱动程序，然后在目标计算机上安装并测试驱动程序。

-   使用 Visual Studio 将驱动程序复制（"部署"）到目标，并在主机上的 Visual Studio 中启动用户模式调试会话。
-   手动将驱动程序复制到目标。 对目标执行用户模式调试。 在此方案中，您手动附加到在目标上运行的驱动程序主机进程的实例。
-   手动将驱动程序复制到目标，然后从主机执行内核模式调试。

可以同时使用后两个配置，同时在目标上运行用户模式调试器，并在主机上运行内核模式调试器。

## <a href="" id="bp"></a>最佳做法


建议使用已附加的内核调试器进行所有 UMDF 驱动程序测试。

下面是建议的设置。 可以手动设置这些设置，也可以使用 WDK 中的[WDF 验证器控件应用程序](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdf-verifier-control-application)（您尚未 wdfverifier）工具来查看或更改这些设置。

-   在 WUDFHost 上启用应用程序验证工具：

    ```cpp
    AppVerif –enable Heaps Exceptions Handles Locks Memory TLS Leak –for WudfHost.exe
    ```

    如果发生异常，应用程序验证工具会将诊断消息发送到调试器并将其中断。

-   启用[驱动程序验证程序](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)。 打开 "**命令提示符**" 窗口（**以管理员身份运行**）。 键入 verifier 以打开驱动程序验证程序管理器。
-   如果使用内核模式调试会话，请设置**HostFailKdDebugBreak** ，使反射器在终止驱动程序主机进程之前进入内核模式调试器。 默认情况下，此设置在 UMDF 版本1.11 中启用。

-   通过将**UmdfHostProcessSharing**设置为**ProcessSharingDisabled**来禁用池。 有关信息，请参阅[在 INF 文件中指定 WDF 指令](specifying-wdf-directives-in-inf-files.md)。
-   默认情况下，当 UMDF 设备出现故障时，框架会尝试将其重新启动5次。 可以通过将**DebugModeFlags**设置为0x01 来关闭自动重启。 有关详细信息，请参阅[用于调试 WDF 驱动程序的注册表值](registry-values-for-debugging-kmdf-drivers.md)。
-   重新启动计算机。

## <a name="using-visual-studio-with-f5-to-attach-automatically-user-mode-debugging"></a>使用带有 F5 的 Visual Studio 自动附加（用户模式调试）


您必须先设置并配置测试计算机，然后才能将 Visual Studio 与 WDK 一起使用，以便在测试计算机上调试驱动程序。 有关如何执行此操作的信息，请参阅将[驱动程序部署到测试计算机](https://docs.microsoft.com/windows-hardware/drivers)。

配置测试计算机后，请在主计算机上使用 Visual Studio 在你的驱动程序中设置断点。 按 F5 时，Visual Studio 将生成驱动程序，将其部署到目标计算机，并启动用户模式调试会话。

使用此方法部署 UMDF 驱动程序时，Visual Studio 将为该驱动程序启用*umdf 调试模式*。 默认情况下，调试模式意味着：

-   该驱动程序在其自己的专用主机进程内启动。 已关闭[设备池](using-device-pooling-in-umdf-drivers.md)。
-   驱动程序崩溃后，不会自动重新启动设备，并禁用错误报告。
-   此框架不会强制执行在 UMDF 中的[主机进程超时](how-umdf-enforces-time-outs.md)中所述的超时。
-   如果 UMDF 主机进程或框架验证器检测到无效操作，则将在用户模式调试器中中断。

即使驱动程序安装需要重新启动，也可以使用调试模式来调试 UMDF 驱动程序。 你还可以调试在用户登录前启动的用户模式驱动程序，例如，生物识别、智能卡或输入。

## <a name="using-windbg-to-attach-manually-user-mode-debugging"></a>使用 WinDbg 手动附加（用户模式调试）


在目标计算机上，可以手动将 WinDbg 附加到承载驱动程序的 WUDFHost 的实例。 附加时，将中断调试器，可以在驱动程序中设置断点。

由于驱动程序初始化在 WUDFHost 加载之后不久就会发生，因此，在调试初始化代码时手动附加是不切实际的。 相反，你可以设置一个注册表值，以使主机进程在主机初始化或驱动程序加载时间等待数秒。 此延迟使你有时间将 WinDbg 附加到正确的 WUDFHost 过程实例。

执行以下步骤:

1.  在目标计算机上的注册表中，将 " **HostProcessDbgBreakOnStart** " 或 " **HostProcessDbgBreakOnDriverLoad** " 设置为一定的秒数，然后重新启动。
2.  在目标计算机上，以管理员身份打开 WinDbg。
3.  在 "**文件**" 菜单上，选择 "**附加到进程**"。 选择 "**按可执行文件**"，然后找到名为 WUDFHost 的所有进程（可能不存在）。 如果存在名为 WUDFHost 的任何进程，请记下其进程标识符以供将来参考。
4.  在设备管理器中，启用驱动程序。
5.  重复步骤2，查找 WUDFHost 的新实例。 如果看不到 WUDFHost 的新实例，请单击 "**取消**"，并再次选择 "**附加到进程**"。 找到 WUDFHost 的新实例后，选择它，然后单击 **"确定"** 。

如果正在使用[设备池](using-device-pooling-in-umdf-drivers.md)，并设置了**HostProcessDbgBreakOnDriverLoad**注册表值，则可能会由于加载其他驱动程序而导致调试器中断。 可以使用 UMDF 调试模式关闭设备池。

若要使用调试模式，请使用 Visual Studio 中的 F5 选项，或在注册表中设置**DebugModeFlags**和**DebugModeBinaries**值。

有关 UMDF 注册表值的详细信息，请参阅[用于调试 WDF 驱动程序的注册表值（KMDF 和 UMDF）](registry-values-for-debugging-kmdf-drivers.md)。

## <a href="" id="kd"></a>使用 WinDbg 从主机远程调试（内核模式调试）


在远程主机上，建立一个内核模式调试会话，然后将当前进程设置为托管驱动程序的 Wudfhost 的实例。 如果是从远程内核调试器进行调试，则可以将**HostProcessDbgBreakOnDriverStart**或**HostProcessDbgBreakOnDriverLoad**设置为0x80000000，以指定无超时，但进入内核调试器。

在 UMDF 1.11 或更高版本中，在侵入内核调试器之前，反射器会自动将进程上下文切换为主机进程的上下文。 因此，你可以立即使用 UMDF 调试器扩展命令，而无需首先发出[**process**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-process--set-process-context-)命令来更改进程上下文。

使用以下步骤：

1. 禁用池。 在**DebugModeBinaries**中打开**DebugModeFlags**并列出你的驱动程序
2. 如果驱动程序使用 UMDF 1.11 或更高版本，则默认情况下会启用**HostFailKdDebugBreak** 。 跳过此步骤。

   如果驱动程序使用 UMDF 1.9 或更早版本，请将**HostFailKdDebugBreak**设置为1。

3. 如果要调试与超时相关的问题，请关闭**HostProcessDbgBreakOnDriverStart**和**HostProcessDbgBreakOnDriverLoad**。 （当**HostProcessDbgBreakOnDriverStart**或**HostProcessDbgBreakOnDriverLoad**为非零时，framework 禁用超时，以便在用户模式调试器附加到主机进程时，反射器不会终止宿主。）如果需要调试驱动程序初始化代码，而不是使用这两个值，请在您的驱动程序加载之前尝试在 WinDbg 中发出以下命令： **sxe ld：** <em>MyDriver</em> （模块加载时中断）
4. 如果进行了任何注册表更改，则重新启动。
5. 根据前面所做的选择，当驱动程序在目标上加载或卸载时，远程内核调试器应该会中断。

 

 





