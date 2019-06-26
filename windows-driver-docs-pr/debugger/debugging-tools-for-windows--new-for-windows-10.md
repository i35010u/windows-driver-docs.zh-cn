---
title: 对于 Windows 10 的新的 Windows 调试工具
description: 适用于 Windows 10 的 Windows 调试工具包括这些新功能。
ms.assetid: DCF1222F-6A67-463E-8C31-B7753CAFFC20
ms.date: 01/22/2019
ms.localizationpriority: medium
ms.openlocfilehash: bd7de9b8754ad6d71e1e32c0e9cc479d10c116ce
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366919"
---
# <a name="debugging-tools-for-windows-new-for-windows-10"></a>Windows 调试工具：Windows 10 的新增功能

## <a name="span-idwindbgpreviewspanspan-idwindbgpreviewspanspan-idwindbgpreviewspanwindbg-preview"></a><span id="Windbg_Preview"></span><span id="windbg_preview"></span><span id="WINDBG_PREVIEW"></span>Windbg 预览

有关 Windows 调试工具的最新新闻，请参阅[WinDbg 预览版-What's New](windbg-what-is-new-preview.md)。


## <a name="span-idwindows10version1703spanspan-idwindows10version1703spanspan-idwindows10version1703spanwindows10-version-1703"></a><span id="Windows_10__version_1703"></span><span id="windows_10__version_1703"></span><span id="WINDOWS_10__VERSION_1703"></span>Windows 10，版本 1703

本部分介绍在 Windows 10，版本 1703年中的新调试工具。

-   八个新的 JavaScript 主题包括[JavaScript 调试器脚本](javascript-debugger-scripting.md)
-   更新到[ **dx （显示调试器对象模型表达式）** ](dx--display-visualizer-variables-.md)命令，以包含新的命令功能。
-   新[ **dtx （显示类型的扩展的调试器对象模型信息）** ](dtx--display-type---extended-debugger-object-model-information-.md)命令。
-   新[ **！ ioctldecode** ](-ioctldecode.md)命令。
-   更新[调试器引擎参考](https://docs.microsoft.com/windows-hardware/drivers/debugger/debugger-engine-reference)以包括其他接口和结构。
-   更新到[配置 tools.ini](configuring-tools-ini.md)到文档的命令行调试器的其他选项。
-   发布中的 75 先前未记录的停止代码[Bug 检查代码参考](bug-check-code-reference2.md)。
-   新[有关在 Windows 10 中的网络内核调试支持以太网 Nic](supported-ethernet-nics-for-network-kernel-debugging-in-windows-10.md)主题。

## <a name="span-idwindows10version1607spanspan-idwindows10version1607spanspan-idwindows10version1607spanwindows10-version-1607"></a><span id="Windows_10__version_1607"></span><span id="windows_10__version_1607"></span><span id="WINDOWS_10__VERSION_1607"></span>Windows 10，版本 1607


本部分介绍在 Windows 10，版本 1607年中的新调试工具。

-   有关新主题[调试 UWP 应用使用 WinDbg](debugging-a-uwp-app-using-windbg.md)。
-   更新到 30 查看次数最多的开发人员 bug 签入主题[Bug 检查代码参考](bug-check-code-reference2.md)。


## <a name="span-idwindows10spanspan-idwindows10spanspan-idwindows10spanwindows10"></a><span id="Windows_10"></span><span id="windows_10"></span><span id="WINDOWS_10"></span>Windows 10

-   [ **（将调试设置）.settings** ](-settings--set-debug-settings-.md) -新的命令，可用于设置、 修改、 显示、 加载和保存 Debugger.Settings 命名空间中的设置。
-   [**dx （显示 NatVis 表达式）** ](dx--display-visualizer-variables-.md) -描述新的 dx 调试器命令，支持使用 NatVis 扩展模型和 LINQ 的显示对象信息。
-   使用调试程序环境中的 NatVis 可视化效果文件的新命令。
    -   [ **.nvlist （NatVis 列表）** ](-nvlist--natvis-list-.md)
    -   [ **.nvload （NatVis 加载）** ](-nvload--natvis-load-.md)
    -   [ **.nvunload (NatVis Unload)** ](-nvunload--natvis-unload-.md)
    -   [ **.nvunloadall （NatVis 卸载所有）** ](-nvunloadall--natvis-unload-all-.md)
-   [蓝牙扩展 (Bthkd.dll)](bluetooh-extensions--bthkd-dll-.md)
-   [存储内核调试器扩展](storage-kernel-debugger-extensions.md)
-   新 Symproxy 信息，包括[SymProxy Automated Installation](symproxy-automated-installation.md)。 此外，以下主题会更新以涵盖新 SymProxy 功能：
    -   [HTTP 符号存储区](http-symbol-stores.md)
    -   [SymProxy](symproxy.md)
    -   [安装 SymProxy](installing-symproxy.md)
    -   [配置注册表](configuring-the-registry.md)
    -   [为 SymProxy 配置 IIS](configuring-iis-for-symproxy.md)
-   [**CDB 命令行选项**](cdb-command-line-options.md) -经过更新以包括新的命令行选项。
-   [ **！ 分析**](-analyze.md) -经过更新以包括有关此扩展与 UMDF 2.15 配合使用的信息。
-   [ **！ wdfkd.wdfcrashdump**](-wdfkd-wdfcrashdump.md)-经过更新以包括有关使用此扩展和 UMDF 2.15 信息
-   [ **！ irp** ](-irp.md) -已更新。 从 Windows 10 开始 IRP 主版本号和次代码文本显示在命令输出中。
-   [使用调试器标记语言](debugger-markup-language-commands.md)-经过更新以说明新右键单击可用调试器标记语言 (DML) 中的行为。
-   [故障转储分析使用 Windows 调试器 (WinDbg)](crash-dump-files.md) -接管 KDNET 内存转储中增加了性能。
-   [调试步骤的实验室 （Echo 内核模式） 的通用驱动程序-](debug-universal-drivers---step-by-step-lab--echo-kernel-mode-.md)-新的执行步骤的实验，演示了如何使用 WinDbg 调试示例 KMDF echo 驱动程序。

 
## <a name="looking-to-download-the-debugging-tools"></a>想要下载调试工具？

下载调试工具的信息，请参阅[的 Windows 中下载调试的工具](debugger-download-tools.md)。



