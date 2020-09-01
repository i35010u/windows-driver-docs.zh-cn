---
title: 使用 Visual Studio 进行调试
description: 从 Windows 驱动程序工具包开始 (WDK) 8，驱动程序开发环境和 Windows 调试器集成到 Microsoft Visual Studio 中。
ms.assetid: B961B0C9-FF6C-4F6B-AC15-CA1B405A4C4C
ms.date: 05/11/2018
ms.localizationpriority: medium
ms.openlocfilehash: 6ab080fbb8a0dc4ba976155013aded38d76aa7bd
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89214832"
---
# <a name="debugging-using-visual-studio"></a>使用 Visual Studio 进行调试

从 Windows 驱动程序工具包开始 (WDK) 8，驱动程序开发环境和 Windows 调试器集成到 Microsoft Visual Studio 中。 在此集成环境中，Visual Studio 用户界面中提供了编码、构建、打包、测试、调试和部署驱动程序所需的大多数工具。

> [!IMPORTANT]
> 此功能在 Windows 10 版本1507及更高版本的 WDK 中不可用。
>
 
若要获取集成环境，请首先安装 Visual Studio，然后 (WDK) 安装 Windows 驱动程序工具包。 有关详细信息，请参阅 [下载 Windows 驱动程序工具包 (WDK) ](../download-the-wdk.md)。

通常内核模式调试需要两台计算机。 调试程序在主计算机  上运行，所调试的代码在目标计算机  上运行。 目标计算机也称为“测试计算机”  。 您可以在一台计算机上执行用户模式调试，但在某些情况下，您可能需要调试在单独的目标计算机上运行的用户模式进程。

在 Visual Studio 环境中，你可以将目标计算机配置为内核模式和用户模式调试。 你可以建立内核模式调试会话。 您可以附加到用户模式进程，或在主计算机或目标计算机上启动和调试用户模式进程。 可以分析转储文件。 在 Visual Studio 中，你可以在目标计算机上对驱动程序进行签名、部署、安装和加载。

这些主题说明了如何使用 Visual Studio 执行用于调试驱动程序的几项任务。

## <a name="span-idin_this_sectionspanin-this-section"></a><span id="in_this_section"></span>本部分中的内容


-   [使用 Visual Studio 调试用户模式进程](debugging-a-user-mode-process-using-visual-studio.md)
-   [使用 Visual Studio 打开转储文件](opening-a-crash-dump-file-using-visual-studio.md)
-   [在 Visual Studio 中进行内核模式调试](performing-kernel-mode-debugging-using-visual-studio.md)
-   [在 Visual Studio 中结束调试会话](ending-a-debugging-session-in-visual-studio.md)
-   [在 Visual Studio 中设置符号和可执行映像路径](setting-symbol-and-source-paths-in-visual-studio.md)
-   [使用 Visual Studio 进行远程调试](remote-debugging-using-visual-studio.md)
-   [在 Visual Studio 中输入调试器命令](entering-debugger-commands-in-visual-studio.md)
-   [在 Visual Studio 中设置断点](setting-breakpoints-in-visual-studio.md)
-   [在 Visual Studio 中查看调用堆栈](viewing-the-call-stack-in-visual-studio.md)
-   [在 Visual Studio 中调试源代码](viewing-source-and-assembly-code-in-visual-studio.md)
-   [在 Visual Studio 中查看和编辑内存与寄存器](viewing-memory--variables--and-registers-in-visual-studio.md)
-   [在 Visual Studio 中控制线程和进程](viewing-threads-and-processes-in-visual-studio.md)
-   [在 Visual Studio 中配置异常和事件](configuring-exceptions-and-events-in-visual-studio.md)
-   [在 Visual Studio 中保存日志文件](keeping-a-log-file-in-visual-studio.md)

 

