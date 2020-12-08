---
title: 如何启用对 UMDF 驱动程序的调试
description: 如何启用对 UMDF 驱动程序的调试
keywords:
- 调试器 WDK UMDF
- 调试器 WDK UMDF，启用
- User-Mode Driver Framework WDK，启用调试器
- UMDF WDK，启用调试器
- 用户模式驱动程序 WDK UMDF，启用调试器
- 调试驱动程序 WDK UMDF，启用调试器
- 驱动程序调试 WDK UMDF，启用调试器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 074d35b18d08c8204a0430f4143ce2b9fbb70e96
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96814803"
---
# <a name="how-to-enable-debugging-of-a-umdf-driver"></a>如何启用对 UMDF 驱动程序的调试


你可以使用以下配置在开发过程中调试 User-Mode Driver Framework (UMDF) 驱动程序。 所有配置都涉及两台计算机，即主机和目标。 

-   手动将驱动程序复制到目标。 对目标执行用户模式调试。 在此方案中，您手动附加到在目标上运行的驱动程序主机进程的实例。
-   手动将驱动程序复制到目标，然后从主机执行内核模式调试。

建议在附加了内核调试器的情况上进行所有 UMDF 驱动程序测试和开发。

## <a name="best-practices"></a><a href="" id="bp"></a>最佳做法

建议使用已附加的内核调试器进行所有 UMDF 驱动程序测试。

下面是建议的设置。 可以手动设置这些设置，也可以使用 WDK 中的 [WDF 验证器控制应用程序](../devtest/wdf-verifier-control-application.md) ( # A0) 工具来查看或更改这些设置。

-   启用 WUDFHost.exe 上的应用程序验证工具：

    ```cpp
    AppVerif –enable Heaps Exceptions Handles Locks Memory TLS Leak –for WudfHost.exe
    ```

    如果发生异常，应用程序验证工具会将诊断消息发送到调试器并将其中断。

-   如果使用内核模式调试会话，请设置 **HostFailKdDebugBreak** ，使反射器在终止驱动程序主机进程之前进入内核模式调试器。 默认情况下，从 Windows 8 开始启用此设置。

-   通过将 **UmdfHostProcessSharing** 设置为 **ProcessSharingDisabled** 来禁用池。 有关信息，请参阅 [在 INF 文件中指定 WDF 指令](specifying-wdf-directives-in-inf-files.md)。
-   默认情况下，当 UMDF 设备出现故障时，框架会尝试将其重新启动5次。 可以通过将 **DebugModeFlags** 设置为0x01 来关闭自动重启。 有关详细信息，请参阅 [用于调试 WDF 驱动程序的注册表值](registry-values-for-debugging-kmdf-drivers.md)。
-   重新启动计算机。

-   对于调试 UMDF 驱动程序问题，请查看 [确定反射器为何终止了主机进程](determining-why-the-reflector-terminated-the-host-process.md) 并 [调试 UMDF 驱动程序崩溃](debugging-umdf-2-0-drivers.md) 

## <a name="using-windbg-to-attach-manually-user-mode-debugging"></a>使用 WinDbg 手动附加 (用户模式调试) 


在目标计算机上，可以手动将 WinDbg 附加到承载驱动程序的 WUDFHost 的实例。 附加时，将中断调试器，可以在驱动程序中设置断点。

由于驱动程序初始化在 WUDFHost 加载之后不久就会发生，因此，在调试初始化代码时手动附加是不切实际的。 相反，你可以设置一个注册表值，以使主机进程在主机初始化或驱动程序加载时间等待数秒。 此延迟使你有时间将 WinDbg 附加到正确的 WUDFHost 过程实例。

请执行以下步骤：

1.  在目标计算机上的注册表中，将 " **HostProcessDbgBreakOnStart** " 或 " **HostProcessDbgBreakOnDriverLoad** " 设置为一定的秒数，然后重新启动。
2.  在目标计算机上，以管理员身份打开 WinDbg。
3.  在 " **文件** " 菜单上，选择 " **附加到进程**"。 选择 " **按可执行文件**"，并找到名为 WUDFHost.exe 的所有进程 (可能没有任何) 。 如果存在名为 WUDFHost.exe 的任何进程，请记下其进程标识符以供将来参考。
4.  在设备管理器中，启用驱动程序。
5.  重复步骤2，查找 WUDFHost.exe 的新实例。 如果看不到 WUDFHost.exe 的新实例，请单击 " **取消**"，并再次选择 " **附加到进程** "。 找到 WUDFHost.exe 的新实例后，将其选中，然后单击 **"确定"**。

如果正在使用 [设备池](using-device-pooling-in-umdf-drivers.md) ，并设置了 **HostProcessDbgBreakOnDriverLoad** 注册表值，则可能会由于加载其他驱动程序而导致调试器中断。 可以使用 UMDF 调试模式关闭设备池。

若要使用调试模式，请使用 Visual Studio 中的 F5 选项，或在注册表中设置 **DebugModeFlags** 和 **DebugModeBinaries** 值。

有关 UMDF 注册表值的详细信息，请参阅 [用于调试 WDF 驱动程序的注册表值 (KMDF 和 UMDF) ](registry-values-for-debugging-kmdf-drivers.md)。

## <a name="using-windbg-to-remotely-debug-from-a-host-machine-kernel-mode-debugging"></a><a href="" id="kd"></a>使用 WinDbg 远程调试 (内核模式调试的主机) 


在远程主机上，建立一个内核模式调试会话，然后将当前进程设置为托管驱动程序的 Wudfhost 的实例。 如果是从远程内核调试器进行调试，则可以将 **HostProcessDbgBreakOnDriverStart** 或 **HostProcessDbgBreakOnDriverLoad** 设置为0x80000000，以指定无超时，但进入内核调试器。

执行以下步骤：

1. 禁用池。 在 **DebugModeBinaries** 中打开 **DebugModeFlags** 并列出你的驱动程序
2. 如果驱动程序使用 UMDF 1.11 或更高版本，则默认情况下会启用 **HostFailKdDebugBreak** 。 跳过此步骤。

   如果驱动程序使用 UMDF 1.9 或更早版本，请将 **HostFailKdDebugBreak** 设置为1。

3. 如果要调试与超时相关的问题，请关闭 **HostProcessDbgBreakOnDriverStart** 和 **HostProcessDbgBreakOnDriverLoad**。  (当 **HostProcessDbgBreakOnDriverStart** 或 **HostProcessDbgBreakOnDriverLoad** 为非零时，framework 将禁用超时，以便在将用户模式调试器附加到主机进程时，反射器不会终止宿主。 ) 如果需要调试驱动程序初始化代码，而不是使用这两个值，请尝试在你的驱动程序加载之前在 WinDbg 中发出以下命令： **sxe ld：** <em>MyDriver.dll</em>模块加载时 (中断) 
4. 如果进行了任何注册表更改，则重新启动。
5. 根据前面所做的选择，当驱动程序在目标上加载或卸载时，远程内核调试器应该会中断。

 

