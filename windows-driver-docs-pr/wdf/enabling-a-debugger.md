---
title: 如何启用对 UMDF 驱动程序的调试
description: 如何启用对 UMDF 驱动程序的调试
ms.assetid: ea37eb7b-09fa-4c8d-aff7-273b07bc0007
keywords:
- 调试器 WDK UMDF
- 调试器 WDK UMDF，启用
- 启用调试程序的用户模式驱动程序框架 WDK
- UMDF WDK，启用调试器
- 用户模式驱动程序 WDK UMDF，启用调试器
- 调试驱动程序 WDK UMDF，启用调试器
- 驱动程序调试 WDK UMDF，启用调试器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: afaf1f6e452ecbf784907f87842f6ee64b2e0aac
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368730"
---
# <a name="how-to-enable-debugging-of-a-umdf-driver"></a>如何启用对 UMDF 驱动程序的调试


以下配置可用于调试的用户模式驱动程序框架 (UMDF) 驱动程序。 所有配置涉及都到两台计算机、 主机和目标。 在运行 Microsoft Visual Studio 和 Windows Driver Kit (WDK) 以生成该驱动程序的主机计算机上，然后安装并测试您的驱动程序在目标计算机上。

-   使用 Visual Studio （"部署"） 复制到的目标和用户模式下在 Visual Studio 中的主机上的调试会话启动的驱动程序。
-   手动将驱动程序复制到目标。 执行用户模式下在目标上进行调试。 在此方案中，您手动附加到在目标系统上运行的驱动程序主机进程的实例。
-   手动将驱动程序复制到目标，然后执行从主机的内核模式调试。

您可以使用后一种两个配置一起，在主机上运行目标上的用户模式下调试器和内核模式调试程序。

## <a href="" id="bp"></a>最佳做法


我们建议执行此测试使用内核调试程序附加所有 UMDF 驱动程序。

以下被建议的设置。 可以手动设置这些或使用[WDF 验证程序控件应用程序](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdf-verifier-control-application)WDK 若要查看或更改这些设置中的 (WDFVerifier.exe) 工具。

-   启用 WUDFHost.exe 上的应用程序验证工具：

    ```cpp
    AppVerif –enable Heaps Exceptions Handles Locks Memory TLS Leak –for WudfHost.exe
    ```

    如果发生异常时，应用程序验证器将诊断消息发送到调试器和中的分页符。

-   启用[驱动程序验证程序](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)。 打开**命令提示符**窗口 (**以管理员身份运行**)。 若要打开驱动程序验证程序管理器的类型验证程序。
-   如果使用的内核模式调试会话，设置**HostFailKdDebugBreak** ，以便该发送程序之前终止驱动程序主机进程进入内核模式调试器。 默认情况下启动 UMDF 1.11 版中启用此设置。

-   禁用了通过设置连接池**UmdfHostProcessSharing**到**ProcessSharingDisabled**。 有关信息，请参阅[INF 文件中指定 WDF 指令](specifying-wdf-directives-in-inf-files.md)。
-   默认情况下，当 UMDF 设备失败时，框架尝试在最多五次重新启动它。 可以通过设置来关闭自动重新启动**DebugModeFlags**到 0x01。 有关详细信息，请参阅[调试 WDF 驱动程序的注册表值](registry-values-for-debugging-kmdf-drivers.md)。
-   重新启动计算机。

## <a name="using-visual-studio-with-f5-to-attach-automatically-user-mode-debugging"></a>使用 F5 使用 Visual Studio 将自动附加 （用户模式下调试）


可以使用 WDK 与 Visual Studio 调试在测试计算机上的驱动程序之前，您必须首先设置和配置测试计算机。 有关如何执行此操作的信息，请参阅[部署到测试计算机的驱动程序](https://docs.microsoft.com/windows-hardware/drivers)。

将测试计算机配置后，使用主计算机上 Visual Studio 在您的驱动程序中设置断点。 按 F5 时，Visual Studio 生成该驱动程序、 将其部署到目标计算机，并启动用户模式下调试会话。

Visual Studio 部署时使用此技术的 UMDF 驱动程序，开启*UMDF 调试模式*针对该驱动程序。 默认情况下，调试模式意味着：

-   在其自己的专用的主机进程中启动驱动程序。 [设备池](using-device-pooling-in-umdf-drivers.md)处于关闭状态。
-   将不自动重启设备驱动程序崩溃后并禁用错误报告。
-   框架不会强制中所述的超时[UMDF 中的主机进程超时](how-umdf-enforces-time-outs.md)。
-   如果 UMDF 主机进程或框架验证程序检测到无效的操作，UMDF 强行进入用户模式下调试程序。

可以使用调试模式下调试 UMDF 驱动程序，即使驱动程序安装需要重新启动。 此外可以调试启动，然后在用户登录，例如生物识别、 智能卡或输入的用户模式驱动程序。

## <a name="using-windbg-to-attach-manually-user-mode-debugging"></a>使用 WinDbg 手动附加 （用户模式下调试）


目标计算机上手动将 WinDbg 附加到 WUDFHost 承载该驱动程序的实例。 附加时，在调试器中中断并可以在您的驱动程序中设置断点。

因为驱动程序初始化发生后不久 WUDFHost 加载，不能手动附加要调试初始化代码的时间。 相反，您可以设置注册表值会导致主机进程要等待的秒在主机初始化或驱动程序加载时某些数。 此延迟可以让用户有时间将 WinDbg 附加到正确的 WUDFHost 过程实例。

请执行以下步骤：

1.  在目标计算机上注册表中，设置**HostProcessDbgBreakOnStart**或**HostProcessDbgBreakOnDriverLoad**到一定数量的秒和重新启动。
2.  在目标计算机上以管理员身份打开 WinDbg。
3.  上**文件**菜单中，选择**附加到进程**。 选择**由可执行文件**，并找到名为的 WUDFHost.exe （有可能不是任何） 的所有进程。 如果有任何进程名为 WUDFHost.exe，记下及其进程标识符以供将来参考。
4.  在设备管理器中，启用驱动程序。
5.  重复步骤 2 并找到 WUDFHost.exe 的新实例。 如果看不到 WUDFHost.exe 的新实例，请单击**取消**，然后选择**附加到进程**试。 当查找 WUDFHost.exe 的新实例时，请选择它，并单击**确定**。

如果[设备池](using-device-pooling-in-umdf-drivers.md)在使用中设置**HostProcessDbgBreakOnDriverLoad**注册表值可能会看到调试器中断由于其他驱动程序加载。 您可以关闭设备池使用 UMDF 调试模式。

若要使用调试模式，请在 Visual Studio 中，使用 F5 选项或设置**DebugModeFlags**并**DebugModeBinaries**注册表中的值。

有关 UMDF 注册表值的详细信息，请参阅[调试 WDF 驱动程序 （KMDF 和 UMDF） 的注册表值](registry-values-for-debugging-kmdf-drivers.md)。

## <a href="" id="kd"></a>使用 WinDbg 远程调试从主机计算机 （内核模式调试）


从远程主机建立内核模式调试会话，然后将当前进程设置为 Wudfhost 承载您的驱动程序的实例。 如果从远程内核调试程序调试，则可以设置**HostProcessDbgBreakOnDriverStart**或**HostProcessDbgBreakOnDriverLoad**为 0x80000000 若要指定无超时，但会中断到内核调试器。

在 UMDF 1.11 或更高版本之前中断到内核调试器，该发送程序会自动切换进程上下文的主机进程。 因此，你可以 UMDF 调试器扩展命令立即使用，而无需第一个发出[ **.process** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/-process--set-process-context-)命令以更改进程上下文。

使用以下步骤：

1. 禁用了连接池。 开启**DebugModeFlags** ，并列出您的驱动程序中**DebugModeBinaries**
2. 如果您的驱动程序使用 1.11 或更高版本，UMDF **HostFailKdDebugBreak**默认情况下启用。 跳过此步骤。

   如果您的驱动程序使用 UMDF 1.9 或更早版本，请设置**HostFailKdDebugBreak**为 1。

3. 如果你正在调试的超时与相关的问题，请关闭**HostProcessDbgBreakOnDriverStart**并**HostProcessDbgBreakOnDriverLoad**。 (当**HostProcessDbgBreakOnDriverStart**或**HostProcessDbgBreakOnDriverLoad**为非零，该框架禁用超时，以便该发送程序不会终止时用户模式下的主机调试器已附加到主机进程。）如果需要调试驱动程序初始化代码，而不是使用这两个值，请尝试在驱动程序加载之前在 WinDbg 中执行以下命令： **sxe ld:** <em>MyDriver.dll</em> （在模块加载中断）
4. 如果您所做的任何注册表更改重新启动。
5. 具体取决于上面所做的选择，远程内核调试程序应时中断该驱动程序进行加载或卸载的目标上。

 

 





