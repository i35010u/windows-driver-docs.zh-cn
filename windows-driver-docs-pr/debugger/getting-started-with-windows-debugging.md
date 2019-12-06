---
title: Windows 调试入门
description: 本部分介绍如何开始 Windows 调试。 如果你的目标是使用调试器分析故障转储，请参阅使用 Windows 调试器（WinDbg）进行故障转储分析。
ms.assetid: 4981928E-A33D-4F60-AAA0-124C360B7E03
ms.date: 08/23/2018
ms.localizationpriority: medium
ms.openlocfilehash: 3c12f6b16ab524215892a792dfe02751d66cec3a
ms.sourcegitcommit: ba3199328ea5d80119eafc399dc989e11e7ae1d6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/05/2019
ms.locfileid: "74862170"
---
# <a name="getting-started-with-windows-debugging"></a>Windows 调试入门


本文介绍如何开始 Windows 调试。 如果你的目标是使用调试器分析故障转储，请参阅[使用 WinDbg 分析故障转储文件](crash-dump-files.md)。

若要开始 Windows 调试，请完成本文中所述的任务。

## <a name="1-determine-the-host-and-the-target"></a>1. 确定主机和目标 

调试器在*主机*系统上运行，您要调试的代码在*目标*系统上运行。

   **主机 &lt;--------------------------------------------------&gt; 目标**

![使用双箭头连接的主机和目标 pc](images/targethost1.png)

由于在调试过程中通常会在处理器上停止指令执行，因此通常会使用两台计算机系统。 在某些情况下，您可能能够将虚拟机用作第二个系统。 例如，你可能能够使用与需要调试的代码在同一台电脑上运行的虚拟 PC。 但是，如果你的代码与低级别硬件通信，则使用虚拟 PC 可能不是最佳方法。 有关详细信息，请参阅[设置虚拟机的网络调试-KDNET](setting-up-network-debugging-of-a-virtual-machine-host.md)。

## <a name="2-determine-the-type-kernel-mode-or-user-mode"></a>2. 确定类型：内核模式或用户模式

接下来，需要确定是否将执行内核模式或用户模式调试。

*内核模式*是运行操作系统和特权程序的处理器访问模式。 内核模式代码有权访问系统的任何部分，并且不受限于用户模式代码。 内核模式代码可以访问在用户模式或内核模式下运行的任何其他进程的任何部分。 许多核心操作系统功能和许多硬件设备驱动程序在内核模式下运行。

*用户模式*是指计算机上的应用程序和子系统运行的模式。 在用户模式下运行的进程在其自己的虚拟地址空间内执行此操作。 它们受到限制，无法直接访问系统的多个部分，包括系统硬件、未分配给其使用的内存，以及可能危及系统完整性的系统的其他部分。 由于在用户模式下运行的进程有效地与系统和其他用户模式进程隔离，因此它们不能干扰这些资源。

如果你的目标是调试驱动程序，请确定该驱动程序是内核模式驱动程序还是用户模式驱动程序。 Windows 驱动模型（WDM）驱动程序和内核模式驱动程序框架（KMDF）都是内核模式驱动程序。 作为名称 sugests，用户模式驱动程序框架（UMDF）驱动程序是用户模式驱动程序。

对于某些问题，可能很难确定代码在哪个模式下执行。 在这种情况下，可能需要选取一种模式，并查看该模式下提供了哪些信息。 某些问题需要在用户模式和内核模式下使用调试器。

根据你决定调试的模式，你需要以不同的方式配置和使用调试器。 有些调试命令在这两种模式下的操作都相同，某些命令在不同模式下的操作方式有所不同。

有关在内核模式下使用调试器的信息，请参阅以下文章：
   - [WinDbg 入门（内核模式）](getting-started-with-windbg--kernel-mode-.md) 
   - [调试通用驱动程序-逐步骤实验室（回显内核模式）](debug-universal-drivers---step-by-step-lab--echo-kernel-mode-.md) 
   - [调试驱动程序-逐步骤实验室（Sysvad 内核模式）](debug-universal-drivers--kernel-mode-.md)。 
    
有关在用户模式下使用调试器的信息，请参阅[WinDbg 入门（用户模式）](getting-started-with-windbg.md)。

## <a name="3-choose-your-debugger-environment"></a>3. 选择调试器环境

WinDbg 在大多数情况下都很好，但有时你可能想要使用另一个调试器，如控制台调试器以实现自动化或 Visual Studio。 有关详细信息，请参阅[调试环境](debuggers-in-the-debugging-tools-for-windows-package.md)。

## <a name="4-determine-how-to-connect-the-target-and-host"></a>4. 确定如何连接目标和主机

通常，目标和主机系统由以太网连接。 如果要执行初期工作，或者设备上没有以太网连接，则可以使用其他网络连接选项。 有关详细信息，请参阅以下文章：
   -   [自动设置 KDNET 网络内核调试](setting-up-a-network-debugging-connection-automatically.md)
   -   [设置内核模式调试](setting-up-kernel-mode-debugging-in-windbg--cdb--or-ntsd.md)
   -   [手动设置 KDNET 网络内核调试](setting-up-a-network-debugging-connection.md)
   -   [设置虚拟机的网络调试-KDNET](setting-up-network-debugging-of-a-virtual-machine-host.md)

## <a name="5-choose-either-the-32-bit-or-64-bit-debugging-tools"></a>5. 选择32位或64位调试工具

要选择的调试工具（32位或64位）依赖于在目标和主机系统上运行的 Windows 的版本，以及你是否正在调试32位或64位代码。 有关详细信息，请参阅[选择32位或64位调试工具](choosing-a-32-bit-or-64-bit-debugger-package.md)。

## <a name="6-configure-symbols"></a>6. 配置符号

若要使用 WinDbg 提供的所有高级功能，必须加载适当的符号。 如果未正确配置符号，则在尝试使用依赖于符号的功能时，你将收到一条消息，指示符号不可用。 有关详细信息，请参阅[Windows 调试符号（WinDbg、KD、CDB、NTSD）](symbols.md)。

## <a name="7-configure-source-code"></a>7. 配置源代码

如果你的目标是调试你自己的源代码，你将需要配置你的源代码的路径。 有关详细信息，请参阅[源路径](source-path.md)。

## <a name="8-become-familiar-with-debugger-operation"></a>8. 熟悉调试器操作

本文档的 "[调试器操作](debugger-operation-win8.md)" 一节介绍了各种任务的调试程序操作。 例如，[加载调试器扩展 dll](loading-debugger-extension-dlls.md)介绍了如何加载调试器扩展。 若要了解有关使用 WinDbg 的详细信息，请参阅[使用 windbg 进行调试](debugging-using-windbg.md)。

## <a name="9-become-familiar-with-debugging-techniques"></a>9. 熟悉调试技术

[标准调试技术](standard-debugging-techniques.md)适用于大多数调试方案，例如，设置断点、检查调用堆栈和查找内存泄漏。 [专用调试技术](specialized-debugging-techniques.md)适用于特定技术或代码类型。 示例包括即插即用调试、KMDF 调试和 RPC 调试。

## <a name="10-use-the-debugger-reference-commands"></a>10. 使用调试器引用命令

随着时间的推移，在调试器中工作时，将使用不同的调试命令。 在调试器中使用[ **hh** （打开 HTML 帮助文件）](-hh--open-html-help-file-.md)命令可以显示有关任何调试命令的帮助信息。 有关可用命令的详细信息，请参阅[调试器参考](debugger-reference.md)。

## <a name="11-use-debugging-extensions-for-specific-technologies"></a>11. 使用特定技术的调试扩展

有多个调试扩展可提供特定于域的数据结构的分析。 有关详细信息，请参阅[专用扩展](specialized-extensions.md)。

## <a name="12-learn-about-related-windows-internals"></a>12. 了解相关的 Windows 内部机制

本文档假设你了解 Windows 内部。 若要了解有关 Windows 内部机制的详细信息（包括内存使用情况、上下文、线程和进程），请查看其他资源，例如通过标记 Russinovich、David 所罗门群岛和 Alex Ionescu 的[*Windows 内部机制*](https://docs.microsoft.com/sysinternals/learn/windows-internals)。

## <a name="13-review-additional-debugging-resources"></a>13. 查看其他调试资源

其他资源包括以下书籍和视频：
-  *在 Windows 调试中：通过 Tarik Soulami 的实用调试和跟踪策略*
-   Mario Hewardt 和 Daniel Pravat 的*高级 Windows 调试*
-   [碎片整理工具](https://channel9.msdn.com/Shows/Defrag-Tools)，第13到29个，大约为 WinDbg


## <a name="see-also"></a>另请参阅

-   [WinDbg 入门（内核模式）](getting-started-with-windbg--kernel-mode-.md)
-   [WinDbg 入门（用户模式）](getting-started-with-windbg.md)
-   [选择32位或64位调试工具](choosing-a-32-bit-or-64-bit-debugger-package.md)
-   [调试环境](debuggers-in-the-debugging-tools-for-windows-package.md)
-   [设置调试（内核模式和用户模式）](getting-set-up-for-debugging.md)
-   [调试通用驱动程序-逐步骤实验室（回显内核模式）](debug-universal-drivers---step-by-step-lab--echo-kernel-mode-.md)
-   [调试驱动程序-逐步骤实验室（Sysvad 内核模式）](debug-universal-drivers--kernel-mode-.md)
