---
title: 适用于 windows 10 的 Windows 全新调试工具
description: 对于 Windows 10，Windows 调试工具包含这些新功能。
ms.assetid: DCF1222F-6A67-463E-8C31-B7753CAFFC20
ms.date: 01/22/2019
ms.localizationpriority: medium
ms.openlocfilehash: d51412bd5ae8327b61d0f962e2579672e7521e43
ms.sourcegitcommit: f610410e1500f0b0a4ca008b52679688ab51033d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/15/2020
ms.locfileid: "88252969"
---
# <a name="debugging-tools-for-windows-new-for-windows-10"></a>Windows 调试工具：Windows 10 的新增功能

## <a name="span-idwindbg_previewspanspan-idwindbg_previewspanspan-idwindbg_previewspanwindbg-preview"></a><span id="Windbg_Preview"></span><span id="windbg_preview"></span><span id="WINDBG_PREVIEW"></span>Windbg 预览

有关 Windows 调试工具上的最新新闻，请参阅 [WinDbg 预览版-新增功能](windbg-what-is-new-preview.md)。


## <a name="span-idwindows_10__version_1703spanspan-idwindows_10__version_1703spanspan-idwindows_10__version_1703spanwindows10-version-1703"></a><span id="Windows_10__version_1703"></span><span id="windows_10__version_1703"></span><span id="WINDOWS_10__VERSION_1703"></span>Windows 10 版本1703

本部分介绍 Windows 10 1703 版中的新增调试工具。

-   8个新的 JavaScript 主题，其中包括 [JavaScript 调试器脚本](javascript-debugger-scripting.md)
-   [**Dx (的更新显示调试器对象模型表达式) **](dx--display-visualizer-variables-.md)命令，以包含新的命令功能。
-   新 [**的 dtx (显示类型-扩展调试器对象模型信息) **](dtx--display-type---extended-debugger-object-model-information-.md) 命令。
-   New [**！ ioctldecode**](-ioctldecode.md) 命令。
-   已更新 [调试器引擎引用](debugger-engine-reference.md) 以包含附加接口和结构。
-   用于 [配置 tools.ini](configuring-tools-ini.md) 以记录命令行调试程序的其他选项的更新。
-   [Bug 检查代码引用](bug-check-code-reference2.md)中已发布75以前未记录的停止代码。
-   [适用于 Windows 10 中的网络内核调试的新支持以太网 nic](supported-ethernet-nics-for-network-kernel-debugging-in-windows-10.md)主题。

## <a name="span-idwindows_10__version_1607spanspan-idwindows_10__version_1607spanspan-idwindows_10__version_1607spanwindows10-version-1607"></a><span id="Windows_10__version_1607"></span><span id="windows_10__version_1607"></span><span id="WINDOWS_10__VERSION_1607"></span>Windows 10 版本1607


本部分介绍 Windows 10 1607 版中的新增调试工具。

-   有关 [使用 WinDbg 调试 UWP 应用的](debugging-a-uwp-app-using-windbg.md)新主题。
-   [Bug 检查代码参考](bug-check-code-reference2.md)中最多30个查看的开发人员 bug 检查主题。


## <a name="span-idwindows_10spanspan-idwindows_10spanspan-idwindows_10spanwindows10"></a><span id="Windows_10"></span><span id="windows_10"></span><span id="WINDOWS_10"></span>Windows 10

-   [**。设置 (设置调试设置) **](-settings--set-debug-settings-.md) -新命令，可用于设置、修改、显示、加载和保存调试程序中的设置。设置命名空间。
-   [**dx (显示 NatVis 表达式) **](dx--display-visualizer-variables-.md) -介绍了新的 dx 调试器命令，该命令使用 NatVis 扩展模型和 LINQ 支持显示对象信息。
-   用于在调试器环境中处理 NatVis 可视化文件的新命令。
    -   [**.nvlist（NatVis 列出）**](-nvlist--natvis-list-.md)
    -   [**.nvload（NatVis 加载）**](-nvload--natvis-load-.md)
    -   [**.nvload（NatVis 卸载）**](-nvunload--natvis-unload-.md)
    -   [**.nvunloadall（NatVis 全部卸载）**](-nvunloadall--natvis-unload-all-.md)
-   [蓝牙扩展 (Bthkd.dll)](bluetooh-extensions--bthkd-dll-.md)
-   [存储内核调试程序扩展](storage-kernel-debugger-extensions.md)
-   新的 Symproxy 信息，包括 [Symproxy 自动安装](symproxy-automated-installation.md)。 此外，还更新了以下主题，以涵盖新的 SymProxy 功能：
    -   [HTTP 符号存储](http-symbol-stores.md)
    -   [SymProxy](symproxy.md)
    -   [安装 SymProxy](installing-symproxy.md)
    -   [配置注册表](configuring-the-registry.md)
    -   [为 SymProxy 配置 IIS](configuring-iis-for-symproxy.md)
-   [**CDB 命令行选项**](cdb-command-line-options.md) -已更新为包含新的命令行选项。
-   [**！分析**](-analyze.md) -更新以包含有关将此扩展与 UMDF 2.15 一起使用的信息。
-   [**！ wdfkd wdfcrashdump**](-wdfkd-wdfcrashdump.md)-已更新为包含有关将此扩展与 UMDF 2.15 一起使用的信息
-   [**！ irp**](-irp.md) -已更新。 从 Windows 10 开始，IRP 主要和次要代码文本显示在命令输出中。
-   [使用调试器标记语言](debugger-markup-language-commands.md) -经过更新以说明新的选择和保留 (或右键单击调试器标记语言 (DML) 中提供) 行为。
-   [使用 Windows 调试器进行故障转储分析 (WinDbg) ](crash-dump-files.md) -在通过 KDNET 进行内存转储时，性能已增加。
-   [调试通用驱动程序-分步实验室 (Echo 内核模式) ](debug-universal-drivers---step-by-step-lab--echo-kernel-mode-.md)-新的循序渐进实验室，演示如何使用 WinDbg 调试示例 KMDF Echo 驱动程序。

 
## <a name="looking-to-download-the-debugging-tools"></a>想要下载调试工具？

有关下载调试工具的信息，请参阅 [下载适用于 Windows 的调试工具](debugger-download-tools.md)。



