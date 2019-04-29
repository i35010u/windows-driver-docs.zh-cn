---
title: 调试环境
description: 从开始使用 Windows Driver Kit (WDK) 8.0，驱动程序开发环境和 Windows 调试器集成到 Microsoft Visual Studio。
ms.assetid: 13F9D82A-4C04-425A-A063-B349DB5C8E08
keywords:
- WinDbg
- KD
- CDB
- NTSD
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0fc765998bf763ac189ab9ddd3618c2b64f30a22
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63324637"
---
# <a name="debugging-environments"></a>调试环境


从开始使用 Windows Driver Kit (WDK) 8.0，驱动程序开发环境和 Windows 调试器集成到 Microsoft Visual Studio。

安装 Visual Studio 和 WDK 后，你会具有六个可用的调试环境：

-   Visual Studio 中使用集成 Windows 调试器
-   Microsoft Windows 调试器 (WinDbg)
-   Microsoft 内核调试程序 (KD)
-   NTKD
-   Microsoft Console Debugger (CDB)
-   Microsoft NT 符号调试器 (NTSD)

以下部分介绍调试环境。

### <a name="span-idvisualstudiowithintegratedwindowsdebuggerspanspan-idvisualstudiowithintegratedwindowsdebuggerspanspan-idvisualstudiowithintegratedwindowsdebuggerspanvisual-studio-with-integrated-windows-debugger"></a><span id="Visual_Studio_with_integrated_Windows_debugger"></span><span id="visual_studio_with_integrated_windows_debugger"></span><span id="VISUAL_STUDIO_WITH_INTEGRATED_WINDOWS_DEBUGGER"></span>Visual Studio 中使用集成 Windows 调试器

从开始使用 WDK 8.0，驱动程序开发环境和 Windows 调试器集成到 Visual Studio。 在此集成环境中，大多数工具所需的编码、 构建、 打包、 测试、 调试和部署驱动程序中提供了 Visual Studio 用户界面。

通常内核模式调试需要两台计算机。 在运行调试程序*主机计算机*和代码正在上调试运行*目标计算机*。 使用 Windows 调试器集成到 Visual Studio，可以执行各种调试任务，包括以下列表中，从主计算机中所示。

-   配置一组用于调试的目标计算机。
-   配置到一组目标计算机的调试连接。
-   启动主计算机和目标计算机之间的内核模式调试会话。
-   调试主机计算机上的用户模式进程。
-   调试目标计算机上的用户模式进程。
-   连接到远程调试会话。
-   查看程序集代码和源代码。
-   查看和操作本地变量、 参数和其他符号。
-   查看和操作的内存。
-   导航的调用堆栈。
-   设置断点。
-   执行调试器命令。

此外可以生成驱动程序、 部署驱动程序和驱动程序从运行的测试在 Visual Studio 用户界面中。 如果要使用的 Visual Studio 集成，提供通过 WDK 和调试工具的 Windows 上，你可以执行几乎所有的驱动程序开发、 打包、 部署、 测试和调试任务从 Visual Studio 中的在主计算机上。 以下是一些已集成到 Visual Studio 的 WDK 功能。

-   配置一组用于驱动程序测试的目标计算机。
-   创建并签署驱动程序包。
-   将驱动程序包部署到目标计算机。
-   安装并加载驱动程序在目标计算机上。
-   测试目标计算机上的驱动程序。

### <a name="span-idwindbgspanspan-idwindbgspanspan-idwindbgspanwindbg"></a><span id="WinDbg"></span><span id="windbg"></span><span id="WINDBG"></span>WinDbg

Microsoft Windows 调试器 (WinDbg) 是一个能够用户模式和内核模式调试的功能强大的基于 Windows 的调试器。 WinDbg 提供了调试的 Windows 内核、 内核模式驱动程序和系统服务，以及用户模式应用程序和驱动程序。

WinDbg 使用 Visual Studio 调试源代码级别调试符号格式。 它可以访问任何符号或变量从模块的 PDB 符号文件，并可以访问由与 COFF 符号文件 （如 Windows.dbg 文件） 编译的模块公开的任何公共函数的名称。

WinDbg 可以查看源代码，设置断点、 查看变量 (包括C++对象)，堆栈跟踪和内存。 其调试器命令窗口中，用户可以发出各种命令。

内核模式调试，WinDbg 通常需要两台计算机 （主机计算机和目标计算机）。 WinDbg 还支持用于用户模式和内核模式目标的各种远程调试选项。

WinDbg 是图形界面对应到 CDB/NTSD 和 KD/NTKD。

### <a name="span-idkdspanspan-idkdspankd"></a><span id="KD"></span><span id="kd"></span>KD

Microsoft Kernel Debugger (KD) 是活动的基于字符的控制台程序，可以深入分析中的内核模式下在所有基于 NT 的操作系统上。 可以使用 KD 可以调试内核模式组件和驱动程序，或监视操作系统本身的行为。 KD 还支持多处理器进行调试。

通常情况下，KD 不运行正在调试的计算机上。 需要两台计算机 (*主机计算机*并*目标计算机*) 内核模式调试。

### <a name="span-idntkdspanspan-idntkdspanntkd"></a><span id="NTKD"></span><span id="ntkd"></span>NTKD

没有名为 NTKD KD 调试器的一种变体。 它等同于 KD 每种方式，不同之处在于它会生成一个新的文本窗口已启动，而 KD 继承命令提示符窗口中调用它。

### <a name="span-idcdbspanspan-idcdbspancdb"></a><span id="CDB"></span><span id="cdb"></span>CDB

Microsoft Console Debugger (CDB) 是一个基于字符的控制台程序，使低级别的 Windows 用户模式内存和构造的分析。 名称*Console Debugger*用于指示这一事实，CDB 分类为一个控制台应用程序; 它并不表示目标应用程序必须是一个控制台应用程序。 事实上，CDB 是完全能够调试控制台应用程序和图形的 Windows 程序。

CDB 是非常强大的调试程序当前正在运行或具有最近崩溃 （实时分析），但简单的设置。 它可用于调查的工作应用程序的行为。 对于失败的应用程序，可以使用 CDB，若要获取堆栈跟踪，或查看犯过参数。 它可以也在 （使用远程访问服务器） 的网络，因为它是基于字符的不同而不同。

使用 CDB，可以显示和执行程序代码、 设置断点，并检查和更改值位于内存中。 CDB 可以通过拆装它并显示程序集指令分析的二进制代码。 它还可以直接分析源代码。

由于 CDB 可以通过地址或全局符号来访问内存位置，你可以引用数据和说明通过名称而不是地址，使其易于查找和调试代码的特定部分。 CDB 支持调试多个线程和进程。 它是可扩展的并可以读取和写入都分页的和非分页内存。

如果目标应用程序本身是一个控制台应用程序，目标将使用 CDB 共享控制台窗口。 若要生成单独的控制台窗口为目标的控制台应用程序，请使用 *-2*命令行选项。

### <a name="span-idntsdspanspan-idntsdspanntsd"></a><span id="NTSD"></span><span id="ntsd"></span>NTSD

没有名为 Microsoft NT 符号调试器 (NTSD) CDB 调试器的一种变体。 它等同于 CDB 每种方式，不同之处在于它会生成一个新的文本窗口已启动，而 CDB 继承命令提示符窗口中调用它。

由于**启动**还可以使用命令来生成新的控制台窗口中，以下两个构造将提供相同的结果：

```console
start cdb parameters 
ntsd parameters
```

则可以重定向输入和输出进行 NTSD （或 CDB），以便它可以控制从内核调试程序 （Visual Studio、 的 WinDbg 中或 KD）。 如果没有控制台窗口将会出现在与 NTSD，则使用此技术。 从内核调试器控制 NTSD 是因此特别有用，因为它产生的使用将几乎没有负担放在包含目标应用程序的计算机的极轻型调试器。 此组合可以用于调试系统进程、 关闭和启动的后面阶段。 请参阅[控制用户模式下调试程序与内核调试程序](controlling-the-user-mode-debugger-from-the-kernel-debugger.md)有关详细信息。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[Windows 调试](index.md)

 

 






