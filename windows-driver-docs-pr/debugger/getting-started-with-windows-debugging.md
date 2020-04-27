---
title: Windows 调试入门
description: 本部分介绍如何开始 Windows 调试。 如果你的目标是使用调试器分析故障转储，请参阅使用 Windows 调试器 (WinDbg) 进行故障转储分析。
ms.assetid: 4981928E-A33D-4F60-AAA0-124C360B7E03
ms.date: 08/23/2018
ms.localizationpriority: high
ms.openlocfilehash: 9e62ff14ef3e006c85bf880a1f27ed885a655bbf
ms.sourcegitcommit: 5598b4c767ab56461b976b49fd75e4e5fb6018d2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2020
ms.locfileid: "78335960"
---
# <a name="getting-started-with-windows-debugging"></a>Windows 调试入门


本文介绍如何开始 Windows 调试。 如果你的目标是使用调试器分析故障转储，请参阅[使用 WinDbg 分析故障转储文件](crash-dump-files.md)。

若要开始 Windows 调试，请完成本文中描述的任务。

## <a name="1-determine-the-host-and-the-target"></a>1.确定主机和目标 

调试器在“主机”系统上运行，要调试的代码在“目标”系统上运行   。

   **主机&lt; --------------------------------------------------&gt;目标**

![用双箭头连接的主机和目标 PC](images/targethost1.png)

由于在调试期间通常会停止处理器上的指令执行，因此通常使用两个计算机系统。 在某些情况下，你可能能够将虚拟机用作第二个系统。 例如，你可以使用与需要调试的代码运行在同一台计算机上的虚拟 PC。 但是，如果你的代码正在与低级硬件通信，则使用虚拟 PC 可能不是最佳方法。 有关详细信息，请参阅[设置虚拟机的网络调试 - KDNET](setting-up-network-debugging-of-a-virtual-machine-host.md).

## <a name="2-determine-the-type-kernel-mode-or-user-mode"></a>2.确定类型：内核模式或用户模式

接下来，需要确定是进行内核模式调试还是用户模式调试。

“内核模式”是处理器访问模式，操作系统和特权程序以此模式运行  。 内核模式代码有权访问系统的任何部分，而不像用户模式代码那样受到限制。 内核模式代码可以访问在用户模式或内核模式下运行的任何其他进程的任何部分。 许多核心操作系统功能和许多硬件设备驱动程序在内核模式下运行。

“用户模式”是计算机上的应用程序和子系统运行的模式  。 在用户模式下运行的进程在其自己的虚拟地址空间中运行。 它们受到限制，无法直接访问系统的许多部分，包括系统硬件、未分配给它们使用的内存以及可能损害系统完整性的系统其他部分。 由于以用户模式运行的进程与系统和其他用户模式进程有效隔离，因此它们不能干扰这些资源。

如果你的目标是调试驱动程序，请确定该驱动程序是内核模式驱动程序还是用户模式驱动程序。 Windows 驱动程序模型 (WDM) 驱动程序与内核模式驱动程序框架 (KMDF) 都是内核模式驱动程序。 顾名思义，用户模式驱动框架（“UMDF”）驱动程序是用户模式驱动程序。

由于某些问题，可能很难确定代码以何种模式执行。 在这种情况下，可能需要选择一种模式并查看在该模式下可用的信息。 有些问题需要在用户模式和内核模式下使用调试器。

根据你决定调试的模式，需要以不同的方式配置和使用调试器。 有些调试命令在两种模式下的操作相同，有些命令在不同模式下的操作不同。

有关在内核模式下使用调试器的信息，请参阅以下文章：
   - [WinDbg 入门（内核模式）](getting-started-with-windbg--kernel-mode-.md) 
   - [调试通用驱动程序 - 分步实验（Echo 内核模式）](debug-universal-drivers---step-by-step-lab--echo-kernel-mode-.md) 
   - [调试驱动程序 - 分步实验（Sysvad 内核模式）](debug-universal-drivers--kernel-mode-.md) 
    
有关在用户模式下使用调试器的信息，请参见 [WinDbg 入门（用户模式）](getting-started-with-windbg.md)

## <a name="3-choose-your-debugger-environment"></a>3.选择调试器环境

WinDbg 在大多数情况下都能正常运行，但有时可能需要使用另一个调试器，例如用于自动化的控制台调试器或 Visual Studio。 有关详细信息，请参阅[调试环境](debuggers-in-the-debugging-tools-for-windows-package.md)。

## <a name="4-determine-how-to-connect-the-target-and-host"></a>4.确定如何连接目标和主机

通常，目标和主机系统通过以太网连接。 如果要执行初期联网工作，或者设备上没有以太网连接，可以使用其他网络连接选项。 有关详细信息，请参阅以下文章：
   -   [自动设置 KDNET 网络内核调试](setting-up-a-network-debugging-connection-automatically.md)
   -   [设置内核模式调试](setting-up-kernel-mode-debugging-in-windbg--cdb--or-ntsd.md)
   -   [手动设置 KDNET 网络内核调试](setting-up-a-network-debugging-connection.md)
   -   [设置虚拟机的网络调试 - KDNET](setting-up-network-debugging-of-a-virtual-machine-host.md)

## <a name="5-choose-either-the-32-bit-or-64-bit-debugging-tools"></a>5.选择 32 位或 64 位调试工具

选择 32 位还是 64 位调试工具，取决于目标系统和主机系统上运行的 Windows 版本，以及所调试的是 32 位还是 64 位代码。 有关详细信息，请参阅[选择 32 位或 64 位调试工具](choosing-a-32-bit-or-64-bit-debugger-package.md)。

## <a name="6-configure-symbols"></a>6.配置符号

若要使用 WinDbg 提供的所有高级功能，必须加载正确的符号。 如果没有正确配置符号，则在尝试使用依赖于符号的功能时，将收到指示符号不可用的消息。 有关详细信息，请参阅 [Windows 调试符号（WinDbg、KD、CDB、NTSD）](symbols.md)

## <a name="7-configure-source-code"></a>7.配置源代码

如果你的目标是调试自己的源代码，则需要配置源代码的路径。 有关详细信息，请参阅[源路径](source-path.md)。

## <a name="8-become-familiar-with-debugger-operation"></a>8.熟悉调试器操作

本文档的[调试器操作](debugger-operation-win8.md)部分描述了各种任务的调试器操作。 例如，[加载调试器扩展 DLL](loading-debugger-extension-dlls.md) 说明了如何加载调试器扩展。 若要了解有关使用 WinDbg 的详细信息，请参阅[使用 WinDbg 进行调试](debugging-using-windbg.md)。

## <a name="9-become-familiar-with-debugging-techniques"></a>9.熟悉调试方法

[标准调试方法](standard-debugging-techniques.md)适用于大多数调试方案，例如，设置断点、检查调用堆栈和查找内存泄漏。 [专业调试方法](specialized-debugging-techniques.md)适用于特定的技术或代码类型。 例如，即插即用调试、KMDF调 试和 RPC 调试。

## <a name="10-use-the-debugger-reference-commands"></a>10.使用调试器引用命令

随着时间的推移，在调试器中工作时将使用不同的调试命令。 使用调试器中的 [.hh](-hh--open-html-help-file-.md)（打开 HTML 帮助文件）命令显示有关任何调试命令的帮助信息  。 有关可用命令的详细信息，请参阅[调试器参考](debugger-reference.md)。

## <a name="11-use-debugging-extensions-for-specific-technologies"></a>11.将调试扩展用于特定技术

有多个调试扩展提供特定于域的数据结构的分析。 有关详细信息，请参阅[专用扩展](specialized-extensions.md)。

## <a name="12-learn-about-related-windows-internals"></a>12.了解相关的 Windows 内部结构

本文档假设你了解 Windows 的内部结构。 若要了解有关 Windows 内部（包括内存使用、上下文、线程和进程）的更多信息，请查看其他资源，如 [Windows 内部结构](https://docs.microsoft.com/sysinternals/learn/windows-internals)（作者：Mark Russinovich、David Solomon 和 Alex Ionescu） 

## <a name="13-review-additional-debugging-resources"></a>13.查看其他调试资源

其他资源包括以下书籍和视频：
-  《在 Windows 调试中：  实用的调试和跟踪策略》，作者：Tarik Soulami
-   《高级 Windows 调试》，作者：Mario Hewardt 和 Daniel Pravat 
-   [碎片整理工具](https://channel9.msdn.com/Shows/Defrag-Tools)第 13 到 29 集，关于 WinDbg


## <a name="see-also"></a>另请参阅

-   [WinDbg 入门（内核模式）](getting-started-with-windbg--kernel-mode-.md)
-   [WinDbg 入门（用户模式）](getting-started-with-windbg.md)
-   [选择 32 位或 64 位调试工具](choosing-a-32-bit-or-64-bit-debugger-package.md)
-   [调试环境](debuggers-in-the-debugging-tools-for-windows-package.md)
-   [设置调试（内核模式和用户模式）](getting-set-up-for-debugging.md)
-   [调试通用驱动程序 - 分步实验（Echo 内核模式）](debug-universal-drivers---step-by-step-lab--echo-kernel-mode-.md)
-   [调试驱动程序 - 分步实验（Sysvad 内核模式）](debug-universal-drivers--kernel-mode-.md)
