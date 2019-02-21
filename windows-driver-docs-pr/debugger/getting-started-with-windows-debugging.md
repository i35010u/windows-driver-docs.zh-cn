---
title: 如何开始使用 Windows 调试
description: 本部分介绍如何开始使用 Windows 调试。 如果你的目标是要使用的调试器来分析故障转储，请参阅使用 Windows 故障转储分析调试器 (WinDbg)。
ms.assetid: 4981928E-A33D-4F60-AAA0-124C360B7E03
ms.date: 08/23/2018
ms.localizationpriority: medium
ms.openlocfilehash: 46df3c5645ea0403f7a10f5ccb757b943bf1ac2a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544678"
---
# <a name="getting-started-with-windows-debugging"></a>如何开始使用 Windows 调试


本部分介绍如何开始使用 Windows 调试。 如果你的目标是要使用的调试器来分析故障转储，请参阅[使用 Windows 故障转储分析调试器 (WinDbg)](crash-dump-files.md)。

若要开始使用 Windows 调试，请完成以下任务。

1. 确定哪些设备将充当主机系统和目标系统。
   调试器在主机系统上运行并在目标系统上运行你想要调试的代码。

   **主机&lt; -------------------------------------------------- &gt;目标**

   ![与双向箭头连接的主机和目标 pc](images/targethost1.png)

   由于很常见，在调试期间停止处理器上的说明执行，因此通常情况下，将使用两个系统。 在某些情况下，很可能第二个系统是一个虚拟系统，例如，在同一台电脑运行的虚拟 PC。 但是，如果你的代码低级别的硬件进行通信，使用 virtual PC 可能不是最佳方法。 有关详细信息，请参阅[设置网络调试的虚拟机主机](setting-up-network-debugging-of-a-virtual-machine-host.md)。

2. 确定是否你将内核或用户模式调试。

   *内核模式*-内核模式是在其中运行的系统和特权程序运行的处理器访问模式。 内核模式代码有权访问的系统，任何部分，并且不受限制用户模式代码等。 它可以访问在用户模式或内核模式中运行的任何其他进程的任何部分。 在内核模式下运行的核心操作系统功能和许多硬件设备驱动程序。

   *用户模式下*-应用程序和子系统在用户模式下在计算机上运行。 在用户模式下运行的进程执行此操作在其自己的虚拟地址空间内。 它们被限制直接访问系统，包括系统硬件，其使用，并可能危及系统完整性的系统的其他部分为未分配的内存的很多部分。 在用户模式下运行的进程是从系统和其他用户模式进程有效地隔离的因为它们不能干扰这些资源。

   如果你的目标是调试驱动程序，确定是否 （通常称为 WDM 或 KMDF 驱动程序） 的内核模式驱动程序或用户模式驱动程序 (UMDF) 驱动程序。

   对于某些问题，它可能很难确定哪种模式中执行代码。 在这种情况下，您可能需要选择一种模式，并查看，可以看到哪些信息是在该模式下可用。 一些问题需要使用用户和内核模式中的调试器。

   根据您决定要调试在什么模式下，将需要配置和调试程序使用不同的方式。 一些调试命令操作相同，并且在不同模式下以不同方式运行一些命令。

   在内核模式中使用调试器的信息，请参阅以下主题：
   - [开始使用 WinDbg （内核模式）](getting-started-with-windbg--kernel-mode-.md) 
   - [调试通用驱动程序的执行步骤的实验室 （Echo 内核模式）](debug-universal-drivers---step-by-step-lab--echo-kernel-mode-.md) 
   - [调试步骤的实验室 （Sysvad 内核模式） 的驱动程序-](debug-universal-drivers--kernel-mode-.md)。 
    
     有关在用户模式下使用调试器的信息，请参阅[开始使用 WinDbg （用户模式）](getting-started-with-windbg.md)。

3. 选择调试程序环境。

   WinDbg 适用于大多数情况下，但您可能的希望使用如控制台调试器自动化或甚至 Visual Studio 的另一个调试器。 有关详细信息，请参阅[调试环境](debuggers-in-the-debugging-tools-for-windows-package.md)。

4. 确定将如何连接的目标和主机系统。

   通常情况下，以太网网络连接用于连接的目标和主机系统。 如果你正在早期启动的工作，或在设备上没有以太网连接，其他网络连接选项都可用。 有关详细信息，请参阅以下主题：
   -   [KDNET 网络内核调试会自动设置](setting-up-a-network-debugging-connection-automatically.md)
   -   [内核模式调试手动设置](setting-up-kernel-mode-debugging-in-windbg--cdb--or-ntsd.md)
   -   [KDNET 网络内核调试手动设置](setting-up-a-network-debugging-connection.md)
   -   [设置网络调试的虚拟机主机](setting-up-network-debugging-of-a-virtual-machine-host.md)

5. 选择任一的 32 位或 64 位调试工具。

   选择此选项是依赖于的目标和主机系统和调试的 32 位或 64 位代码运行的 Windows 版本。 有关详细信息，请参阅[选择 32 位或 64 位调试工具](choosing-a-32-bit-or-64-bit-debugger-package.md)。

6. 配置符号。

   必须加载正确的符号，可以使用所有 WinDbg 提供的高级功能。 如果不具有正确配置的符号，将收到消息，指示的符号不可用时尝试使用依赖于符号的功能。 有关详细信息，请参阅[符号的 Windows 调试 （WinDbg、 KD、 CDB、 NTSD）](symbols.md)。

7. 配置源代码。
   如果你的目标是调试源代码，您需要配置你的源代码的路径。 有关详细信息，请参阅[源路径](source-path.md)。

8. 熟悉调试器操作。
   [调试器操作](debugger-operation-win8.md)文档的部分介绍调试程序的各种任务的操作。 例如，[加载的调试器扩展 Dll](loading-debugger-extension-dlls.md)主题说明如何加载调试器扩展。 若要详细了解如何使用 WinDbg，请参阅[调试使用 WinDbg](debugging-using-windbg.md)。

9. 熟悉的调试技术。
   [标准调试技术](standard-debugging-techniques.md)适用于大多数调试方案和示例包括设置断点、 检查调用堆栈和查找内存泄漏。 [专用化调试技术](specialized-debugging-techniques.md)将应用于特定的技术或类型的代码。 示例包括插调试、 内核模式驱动程序框架调试和 RPC 调试。

10. 使用调试器引用命令。
    随着时间推移，将在调试器中工作时使用不同的调试命令。 使用[.hh （打开 HTML 帮助文件） *](-hh--open-html-help-file-.md)命令，在调试器中以显示有关任何调试命令的帮助信息。 有关可用命令的详细信息，请参阅[调试器参考](debugger-reference.md)。

11. 使用调试特定技术的扩展。
    有大量的调试扩展，用于分析的域特定的数据结构。 有关详细信息，请参阅[专用化扩展插件](specialized-extensions.md)。

12. 了解相关 Windows 内部结构，例如内存使用情况、 上下文、 线程和进程。 本文档假定 Windows 内部结构的知识。 查看资源，例如这本书，若要了解有关 Windows 内部结构的详细信息。 
    -   Mark E.Russinovich、 David A.Solomon 和 Alex Ionescu Windows 内部结构

13. 查看其他调试资源。
    -   深入了解 Windows 调试：调试和跟踪策略通过 Tarik Soulami Windows® 中的实践指南
    -   高级的 Windows 调试由 Mario Hewardt 和 Daniel Pravat
    -   [碎片整理工具显示 WinDbg 剧集 13 29](https://channel9.msdn.com/Shows/Defrag-Tools)


## <a name="see-also"></a>另请参阅

-   [开始使用 WinDbg （内核模式）](getting-started-with-windbg--kernel-mode-.md)
-   [开始使用 WinDbg （用户模式）](getting-started-with-windbg.md)
-   [选择 32 位或 64 位调试工具](choosing-a-32-bit-or-64-bit-debugger-package.md)
-   [调试环境](debuggers-in-the-debugging-tools-for-windows-package.md)
-   [设置调试 （内核模式和用户模式下）](getting-set-up-for-debugging.md)
-   [调试通用驱动程序的执行步骤的实验室 （Echo 内核模式）](debug-universal-drivers---step-by-step-lab--echo-kernel-mode-.md)
-   [调试驱动程序的执行步骤的实验室 （Sysvad 内核模式）](debug-universal-drivers--kernel-mode-.md)



