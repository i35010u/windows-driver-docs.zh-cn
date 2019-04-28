---
title: 使用 Visual Studio 进行调试
description: 开始使用 Windows Driver Kit (WDK) 8、 驱动程序开发环境和调试器集成到 Microsoft Visual Studio Windows。
ms.assetid: B961B0C9-FF6C-4F6B-AC15-CA1B405A4C4C
ms.date: 05/11/2018
ms.localizationpriority: medium
ms.openlocfilehash: d52bf3207354471280f523c1106664cd2723e516
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63346316"
---
# <a name="debugging-using-visual-studio"></a>使用 Visual Studio 进行调试

开始使用 Windows Driver Kit (WDK) 8、 驱动程序开发环境和调试器集成到 Microsoft Visual Studio Windows。 在此集成环境中，大多数工具所需的编码、 构建、 打包、 测试、 调试和部署驱动程序中提供了 Visual Studio 用户界面。

> [!IMPORTANT]
> 此功能不在 Windows 10，版本 1507年和更高版本的 WDK 中可用。
>
 
要获取的集成的环境，请首先安装 Visual Studio 中，然后再安装 Windows Driver Kit (WDK)。 有关详细信息，请参阅[Windows Driver Kit (WDK)](https://go.microsoft.com/fwlink/p?linkid=391063)。

通常内核模式调试需要两台计算机。 调试程序在*主计算机*上运行，所调试的代码在*目标计算机*上运行。 目标计算机也称为*测试计算机*。 你可以执行用户模式下调试上一台计算机，但在某些情况下，你可能想要调试的单独的目标计算机运行的用户模式进程。

在 Visual Studio 环境中，可以配置为内核模式和用户模式下调试目标计算机。 您可以建立一个内核模式调试会话。 可附加到用户模式进程或启动和调试在主计算机或目标计算机上的用户模式进程。 你可以分析转储文件。 在 Visual Studio 中可以登录、 部署、 安装和加载的目标计算机上的驱动程序。

这些主题说明如何使用 Visual Studio 来执行多个调试驱动程序所涉及的任务。

## <a name="span-idinthissectionspanin-this-section"></a><span id="in_this_section"></span>本部分中的内容


-   [调试使用 Visual Studio 的用户模式进程](debugging-a-user-mode-process-using-visual-studio.md)
-   [打开要使用 Visual Studio 的转储文件](opening-a-crash-dump-file-using-visual-studio.md)
-   [内核模式下在 Visual Studio 中调试](performing-kernel-mode-debugging-using-visual-studio.md)
-   [在 Visual Studio 中的调试会话结束](ending-a-debugging-session-in-visual-studio.md)
-   [在 Visual Studio 中设置符号和可执行映像路径](setting-symbol-and-source-paths-in-visual-studio.md)
-   [远程调试使用的 Visual Studio](remote-debugging-using-visual-studio.md)
-   [在 Visual Studio 中输入的调试器命令](entering-debugger-commands-in-visual-studio.md)
-   [在 Visual Studio 中设置断点](setting-breakpoints-in-visual-studio.md)
-   [Visual Studio 中查看调用堆栈](viewing-the-call-stack-in-visual-studio.md)
-   [在 Visual Studio 中调试源代码](viewing-source-and-assembly-code-in-visual-studio.md)
-   [查看和编辑内存和 Visual Studio 中的寄存器](viewing-memory--variables--and-registers-in-visual-studio.md)
-   [控制线程和 Visual Studio 中的进程](viewing-threads-and-processes-in-visual-studio.md)
-   [在 Visual Studio 中配置异常和事件](configuring-exceptions-and-events-in-visual-studio.md)
-   [在 Visual Studio 中保留一个日志文件](keeping-a-log-file-in-visual-studio.md)

 

 





