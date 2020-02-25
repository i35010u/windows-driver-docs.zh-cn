---
title: 调试环境
description: 从 Windows 驱动程序工具包（WDK）8.0 开始，驱动程序开发环境和 Windows 调试器集成到 Microsoft Visual Studio 中。
ms.assetid: 13F9D82A-4C04-425A-A063-B349DB5C8E08
keywords:
- WinDbg
- KD
- CDB
- NTSD
ms.date: 02/20/2020
ms.localizationpriority: medium
ms.openlocfilehash: 5bbaf80898d2007c2b898fa8a4c5db0a2da7f80b
ms.sourcegitcommit: d03c24342b9852013301a37e2ec95592804204f1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/21/2020
ms.locfileid: "77528963"
---
# <a name="debugging-environments"></a>调试环境

有六种可用的调试环境：

- WinDbg Preview
- Windows Debugger (WinDbg)
- 内核调试器（KD）
- NTKD
- 控制台调试器（CDB）
- NT 符号调试器（NTSD）

以下各节介绍了调试环境。

### <a name="span-idwindbgpreviewspanspan-idwindbgpreviewspanspan-idwindbgpreviewspanwindbg-preview"></a><span id="WinDbgPreview"></span><span id="windbgpreview"></span><span id="WINDBGPREVIEW"></span>WinDbg 预览

WinDbg 预览版是最新版本的 WinDbg，具有更多新式视觉对象、更快的 windows，以及使用可扩展调试器数据模型前端和中心构建的完整的脚本编写体验。 现在，WinDbg 预览版使用与 WinDbg 相同的基础引擎，因此你所习惯的所有命令、扩展和工作流的仍然与以前一样使用。

有关详细信息，请参阅[使用 WinDbg Preview 进行调试](debugging-using-windbg-preview.md)

### <a name="span-idwindbgspanspan-idwindbgspanspan-idwindbgspanwindbg"></a><span id="WinDbg"></span><span id="windbg"></span><span id="WINDBG"></span>WinDbg

Microsoft Windows 调试器（WinDbg）是一种基于 Windows 的调试器，它支持用户模式和内核模式调试。 WinDbg 为 Windows 内核、内核模式驱动程序和系统服务以及用户模式应用程序和驱动程序提供调试。

WinDbg 使用 Visual Studio 调试符号格式进行源级别调试。 它可以从包含 PDB 符号文件的模块访问任何符号或变量，并且可以访问由使用 COFF 符号文件（如 Windows dbg 文件）编译的模块公开的任何公共函数名称。

WinDbg 可以查看源代码、设置断点、查看变量（包括C++对象）、堆栈跟踪和内存。 它的调试器命令窗口允许用户发出多种命令。

对于内核模式调试，WinDbg 通常需要两台计算机（主计算机和目标计算机）。 WinDbg 还支持用户模式和内核模式目标的各种远程调试选项。

WinDbg 是与 CDB/NTSD 和 KD/NTKD 对应的图形接口。

### <a name="span-idkdspanspan-idkdspankd"></a><span id="KD"></span><span id="kd"></span>KD

Microsoft 内核调试器（KD）是一种基于字符的控制台程序，可对所有基于 NT 的操作系统上的内核模式活动进行深入分析。 你可以使用 KD 来调试内核模式组件和驱动程序，或监视操作系统本身的行为。 KD 还支持多处理器调试。

通常，KD 不会在正在调试的计算机上运行。 对于内核模式调试，需要两台计算机（*主计算机*和*目标计算机*）。

### <a name="span-idntkdspanspan-idntkdspanntkd"></a><span id="NTKD"></span><span id="ntkd"></span>NTKD

存在名为 NTKD 的 KD 调试器的变体。 它与 KD 的方式完全相同，不同之处在于它在启动时生成新的文本窗口，而 KD 继承从中调用它的命令提示符窗口。

### <a name="span-idcdbspanspan-idcdbspancdb"></a><span id="CDB"></span><span id="cdb"></span>CDB

Microsoft 控制台调试器（CDB）是一个基于字符的控制台程序，可实现对 Windows 用户模式内存和构造的低级别分析。 名称*控制台调试器*用来指示 CDB 分类为控制台应用程序的事实，这并不意味着目标应用程序必须为控制台应用程序。 事实上，CDB 完全能够同时调试控制台应用程序和图形 Windows 程序。

CDB 非常强大，可用于调试当前正在运行或最近崩溃的程序（实时分析），但设置简单。 它可用于调查正在运行的应用程序的行为。 对于发生故障的应用程序，可以使用 CDB 来获取堆栈跟踪，或查看投机取巧参数。 它在网络上非常适合（使用远程访问服务器），因为它是基于字符的。

通过 CDB，你可以显示和执行程序代码、设置断点以及在内存中检查和更改值。 CDB 可以通过对二进制代码进行反汇编并显示程序集说明来对其进行分析。 它还可以直接分析源代码。

由于 CDB 可以通过地址或全局符号访问内存位置，因此可以通过名称而不是按地址来引用数据和说明，从而可以轻松地查找和调试代码的特定部分。 CDB 支持调试多个线程和进程。 它是可扩展的，并且可以读取和写入分页和非分页内存。

如果目标应用程序本身是一个控制台应用程序，则目标将与 CDB 共享控制台窗口。 若要为目标控制台应用程序生成单独的控制台窗口，请使用 *-2*命令行选项。

### <a name="span-idntsdspanspan-idntsdspanntsd"></a><span id="NTSD"></span><span id="ntsd"></span>NTSD

CDB 调试程序有一个名为 "Microsoft NT 符号调试器（NTSD）" 的变体。 它与 CDB 完全相同，不同之处在于它在启动时生成新的文本窗口，而 CDB 继承从中调用该窗口的命令提示符窗口。

由于 "**启动**" 命令还可用于生成新的控制台窗口，因此以下两个构造将产生相同的结果：

```console
start cdb parameters
ntsd parameters
```

可以从 NTSD （或 CDB）重定向输入和输出，以便可以从内核调试器（Visual Studio、WinDbg 或 KD）对其进行控制。 如果此方法与 NTSD 一起使用，则不会显示任何控制台窗口。 因此，从内核调试器控制 NTSD 会特别有用，因为它会导致极轻量的调试程序，这在包含目标应用程序的计算机上几乎没有任何负担。 这种组合可用于调试系统进程、关闭和更高的启动阶段。 有关详细信息，请参阅[从内核调试器控制用户模式调试器](controlling-the-user-mode-debugger-from-the-kernel-debugger.md)。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题

[Windows 调试](index.md)

[使用 WinDbg Preview 进行调试](debugging-using-windbg-preview.md)
