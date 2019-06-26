---
title: 调试资源
description: 使用的 Windows 调试工具来调试驱动程序、 应用程序和 Windows 系统上的服务。
ms.assetid: F2111416-EC6C-4967-B123-9A6101040561
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 687ba28524fc2d972c600c36838a499cfe3ed0ef
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67391974"
---
# <a name="debugging-resources"></a>调试资源


使用的 Windows 调试工具来调试驱动程序、 应用程序和 Windows 系统上的服务。 核心调试引擎中的工具集称为 Windows 调试器。 从 Windows 8 开始，可以使用 Windows 调试器的接口作为 Visual Studio。 此外可以使用传统接口 （WinDbg、 CDB 和 NTSD），该文件包含在为 Windows 调试工具。

## <a name="span-idgettingstartedwithdebuggingtoolsforwindowsspanspan-idgettingstartedwithdebuggingtoolsforwindowsspanspan-idgettingstartedwithdebuggingtoolsforwindowsspangetting-started-with-debugging-tools-for-windows"></a><span id="Getting_Started_with_Debugging_Tools_for_Windows"></span><span id="getting_started_with_debugging_tools_for_windows"></span><span id="GETTING_STARTED_WITH_DEBUGGING_TOOLS_FOR_WINDOWS"></span>入门 Windows 调试工具


-   [Windows 调试](index.md)

## <a name="span-idinstallingdebuggingtoolsforwindowsspanspan-idinstallingdebuggingtoolsforwindowsspanspan-idinstallingdebuggingtoolsforwindowsspaninstalling-debugging-tools-for-windows"></a><span id="Installing_Debugging_Tools_for_Windows"></span><span id="installing_debugging_tools_for_windows"></span><span id="INSTALLING_DEBUGGING_TOOLS_FOR_WINDOWS"></span>安装适用于 Windows 调试工具


-   [下载并安装 Windows 调试工具](https://msdn.microsoft.com/windows/hardware/gg463009)

## <a name="span-iddebuggerhow-tosspanspan-iddebuggerhow-tosspanspan-iddebuggerhow-tosspandebugger-how-tos"></a><span id="Debugger_How-Tos"></span><span id="debugger_how-tos"></span><span id="DEBUGGER_HOW-TOS"></span>调试器注意事项


-   [高级驱动程序调试：第 1 部分\[媒体文件\]](https://download.microsoft.com/download/B/1/6/B161948D-EDE1-4AEF-8776-AD485CDDCD9E/TDDR05003.wvx)
-   [高级驱动程序调试：第 2 部分\[媒体文件\]](https://download.microsoft.com/download/B/1/6/B161948D-EDE1-4AEF-8776-AD485CDDCD9E/TDDR05004.wvx)
-   [避免调试器搜索不需要的符号](https://docs.microsoft.com/windows-hardware/drivers/debugger/avoiding-debugger-searches-for-unneeded-symbols)
-   [调试 Kernel-mode Driver Framework 驱动程序](https://docs.microsoft.com/windows-hardware/drivers/wdf/debugging-kernel-mode-driver-framework-drivers)
-   [调试 WDF 驱动程序](https://docs.microsoft.com/windows-hardware/drivers/wdf/debugging-a-wdf-driver)
-   [如何在各种驱动程序和子系统中启用详细调试跟踪](https://support.microsoft.com/en-us)
-   [调试驱动程序](https://docs.microsoft.com/windows-hardware/drivers)
-   [**BCDEdit /dbgsettings**](https://docs.microsoft.com/windows-hardware/drivers/devtest/bcdedit--dbgsettings)
-   [驱动程序调试工具](https://docs.microsoft.com/windows-hardware/drivers/devtest/tools-for-debugging-drivers)（WDK 文档）

## <a name="span-idknowledgebasearticlesfordebuggingspanspan-idknowledgebasearticlesfordebuggingspanspan-idknowledgebasearticlesfordebuggingspanknowledge-base-articles-for-debugging"></a><span id="Knowledge_base_articles_for_debugging"></span><span id="knowledge_base_articles_for_debugging"></span><span id="KNOWLEDGE_BASE_ARTICLES_FOR_DEBUGGING"></span>用于调试的知识库文章


大量[知识库文章](https://support.microsoft.com/en-us)可用于调试的相关的主题。 此页提供用于调试相关的产品支持链接的几个的示例。

-   [2816225:启用调试模式会导致 Windows，如果没有调试器连接](https://support.microsoft.com/help/2816225/enabling-debug-mode-causes-windows-to-hang-if-no-debugger-is-connected/)
-   [311503:使用 Microsoft 符号服务器获取调试符号文件](https://support.microsoft.com/help/311503)
-   [Q248413:信息：NDIS 内核调试器扩展](https://support.microsoft.com/help/248413)
-   [Q121366:信息：PDB 和 DBG 文件-它们是什么以及它们如何工作](https://support.microsoft.com/help/121366)
-   [Q121543:设置用于远程调试](https://support.microsoft.com/help/121543)
-   [Q129845:之前调用 Microsoft 的蓝屏准备](https://support.microsoft.com/help/129845)
-   [Q128372:如何从设备驱动程序删除符号](https://support.microsoft.com/help/128372)
-   [Q97858:CTRL + C 异常处理在 WinDbg 下](https://support.microsoft.com/help/97858)
-   [Q102351:调试使用重定向的控制台应用程序](https://support.microsoft.com/help/102351)
-   [Q117559:INF:如何关联 Spid，Kpid，和线程实例](https://support.microsoft.com/help/117559)
-   [Q121434:指定的未经处理的用户模式异常的调试器](https://support.microsoft.com/help/121434)
-   [Q133722:如何调试平面 Thunk](https://support.microsoft.com/help/133722)
-   [Q148220:PRB:调试器报告"警告： 符号的校验和不正确"](https://support.microsoft.com/help/148220)
-   [Q137199:PRB:调试器不能可靠地使用调试注册断点](https://support.microsoft.com/help/137199)
-   [Q100957:PRB:调试由 MS 测试驱动的应用程序](https://support.microsoft.com/help/100957)
-   [Q130667:PRB:F12 原因硬编码断点异常时调试](https://support.microsoft.com/help/130667)
-   [Q173260:PRB:调试时的同步失败](https://support.microsoft.com/help/173260)
-   [Q168609:如何使用显示堆 (DH。EXE) 实用程序](https://support.microsoft.com/help/168609)
-   [Q103861:信息：选择的调试程序将生成系统](https://support.microsoft.com/help/103861)

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[DebugView 监视工具](https://technet.microsoft.com/sysinternals/bb896647.aspx)

[驱动程序开发人员社区资源](https://msdn.microsoft.com/windows/hardware/gg454517)

[Windows 驱动程序签名要求](https://docs.microsoft.com/previous-versions/windows/hardware/design/dn653563(v=vs.85))

[对开发人员工具包和工具的支持](https://docs.microsoft.com/previous-versions/gg454528(v=msdn.10))

 

 






