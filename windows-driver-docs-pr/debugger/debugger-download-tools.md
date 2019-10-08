---
title: 下载 Windows 调试工具 - WinDbg
description: 本页提供 Windows 调试工具（如 WinDbg）的下载。
keywords:
- Windows 调试下载
- WinDbg
- 下载
ms.date: 07/02/2019
ms.localizationpriority: High
ms.openlocfilehash: 9f60a3cedcae29bb2366833e77bef50d5761ca92
ms.sourcegitcommit: c73954a5909ec8c7e189f77fd5813f2eb749687c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/07/2019
ms.locfileid: "72007549"
---
# <a name="download-debugging-tools-for-windows"></a>下载适用于 Windows 的调试工具

可以使用 Windows 调试器（WinDbg）调试内核模式和用户模式代码，分析故障转储并在代码执行时检查 CPU 寄存器。

## <a name="small-windbg-preview-logoimageswindbgx-preview-logopng-download-windbg-preview"></a>![小型 windbg 预览徽标](images/windbgx-preview-logo.png) 下载 WinDbg 预览版

WinDbg Preview 是 WinDbg 的新版本，在重要位置构建有可扩展的调试器数据模型，具有更现代的视觉效果、更快速的 Windows 和成熟的脚本体验。 现在，WinDbg Preview 使用与 WinDbg 相同的基础引擎，因此所有命令、扩展和工作流的运行仍然与从前相同。

 - 从 Microsoft Store 下载 WinDbg 预览版：[WinDbg 预览](https://www.microsoft.com/store/p/windbg/9pgjgd53tn86)。

 - 有关详细信息，请参阅[WinDbg 预览版](https://docs.microsoft.com/windows-hardware/drivers/debugger/windbg-install-preview)中的安装和配置。

## <a name="small-classic-windbg-preview-logoimageswindbg-classic-logopng-debugging-tools-for-windows-10-windbg"></a>![小型经典 windbg 预览徽标](images/windbg-classic-logo.png) Windows 10 调试工具 (WinDbg)

如果你只需要适用于 windows 10 的调试工具，而不需要适用于 Windows 10 或 Visual Studio 2017 的 Windows 驱动程序工具包（WDK），则可以将调试工具作为独立组件安装在 Windows SDK 中。 在 SDK 安装向导中，选择 "**适用于 Windows 的调试工具**"，然后取消选择所有其他组件。

 - 从 SDK 获取适用于 Windows 的调试工具（WinDbg）：[Windows 10 SDK](https://developer.microsoft.com/windows/downloads/windows-10-sdk)。

 - 在[适用于 Windows 的调试工具（WinDbg、KD、CDB、NTSD）](https://docs.microsoft.com/windows-hardware/drivers/debugger/)中了解有关 WinDbg 和其他调试程序的详细信息。

> [!TIP]
> 如果 Windows SDK 已安装，请打开 "**设置**"，导航到 "**应用" & 功能**"，选择" **Windows 软件开发工具包**"，然后单击"**修改**"以更改安装以添加**Windows 调试工具**.

-------------------

## <a name="looking-for-the-debugging-tools-for-earlier-version-of-windows"></a>正在查找适用于早期版本的 Windows 的调试工具？

若要下载适用于以前版本的 Windows 的调试器工具，需要从[Windows SDK 和模拟器存档](https://developer.microsoft.com/windows/downloads/sdk-archive)下载正在调试的版本的 Windows SDK。 在 SDK 的安装向导中，选择 "**适用于 Windows 的调试工具**"，然后取消选择所有其他组件。

## <a name="looking-for-related-downloads"></a>查找相关下载？

 - [Windows 驱动程序工具包 (WDK)](https://docs.microsoft.com/windows-hardware/drivers/download-the-wdk)

 - [Windows 调试器符号](debugger-download-symbols.md)  

 - [Windows HLK、HCK 或徽标工具包](https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit)

 - [Windows 评估和部署工具包（Windows ADK）](https://docs.microsoft.com/windows-hardware/get-started/adk-install)

 - [Windows 预览体验预览版本](https://insider.windows.com/)
