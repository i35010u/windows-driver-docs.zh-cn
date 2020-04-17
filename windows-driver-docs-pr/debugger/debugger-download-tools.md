---
title: 下载 Windows 调试工具 - WinDbg
description: 本页提供 Windows 调试工具（如 WinDbg）的下载。
keywords:
- Windows 调试工具下载
- WinDbg
- 下载
ms.date: 04/09/2020
ms.localizationpriority: High
ms.openlocfilehash: 65136ac7f480e07fa1f8e4bd588fcba88e03d6dc
ms.sourcegitcommit: 84be9e06fd0886598df77dffcbc75632d613c8f3
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/11/2020
ms.locfileid: "81208031"
---
# <a name="download-debugging-tools-for-windows"></a>下载 Windows 调试工具

Windows 调试程序 (WinDbg) 可用于调试内核模式和用户模式代码、分析故障转储以及在代码执行时检查 CPU 寄存器。

若要开始使用 Windows 调试，请参阅 [Windows 调试入门](getting-started-with-windows-debugging.md)。

## <a name="small-windbg-preview-logo-download-windbg-preview"></a>![小的 WinDbg Preview 徽标](images/windbgx-preview-logo.png) 下载 WinDbg Preview

WinDbg Preview 是 WinDbg 的新版本，具有更现代的视觉效果、更快速的 Windows 和成熟的脚本体验。 它是在重要位置使用可扩展的面向对象的调试程序数据模型构建的。 现在，WinDbg Preview 使用与 WinDbg 相同的基础引擎，因此所有命令、扩展和工作流的运行仍然与从前相同。

 - 从 Microsoft Store 下载 WinDbg Preview：[WinDbg Preview](https://www.microsoft.com/store/p/windbg/9pgjgd53tn86)。

 - 在 [WinDbg Preview - 安装](https://docs.microsoft.com/windows-hardware/drivers/debugger/windbg-install-preview)中了解有关安装和配置的详细信息。

## <a name="small-classic-windbg-preview-logo-debugging-tools-for-windows-10-windbg"></a>![小的经典 WinDbg Preview 徽标](images/windbg-classic-logo.png) Windows 10 调试工具 (WinDbg)

从 SDK 获取 Windows 调试工具 (WinDbg)：[Windows 10 SDK](https://developer.microsoft.com/windows/downloads/windows-10-sdk)。

如果仅需 Windows 调试工具，而不需适用于 Windows 10 的 Windows 驱动程序工具包 (WDK)，则可将调试工具作为 Windows 软件开发工具包 (SDK) 中的独立组件进行安装。

在 SDK 安装向导中选择“Windows 调试工具”  ，并取消选择所有其他组件。

![SDK 下载选项，仅显示已选中的调试程序框](images/debugger-download-sdk.png)

### <a name="adding-the-debugging-tools-for-windows-if-the-sdk-is-already-installed"></a>如果已安装 SDK，则添加用于 Windows 的调试工具

如果 Windows SDK 已安装，请打开“设置”  ，导航到“应用和功能”  ，选择“Windows 软件开发工具包”  ，然后单击“修改”  对安装进行更改，以便添加“Windows调试工具”。 

-------------------

## <a name="looking-for-the-debugging-tools-for-earlier-versions-of-windows"></a>要查找早期版 Windows 的调试工具？

若要下载旧版 Windows 的调试程序工具，需要从 [Windows SDK 和模拟器存档](https://developer.microsoft.com/windows/downloads/sdk-archive)下载适用于所要调试的版本的 Windows SDK。 在 SDK 的安装向导中选择“Windows 调试工具”  ，并取消选择所有其他组件。

## <a name="learn-more-about-the-debuggers"></a>详细了解调试程序

在 [Windows 调试工具（WinDbg、KD、CDB、NTSD）](https://docs.microsoft.com/windows-hardware/drivers/debugger/)中详细了解 WinDbg 和其他调试程序。

## <a name="looking-for-related-downloads"></a>查找相关下载？

- [下载 Windows 驱动程序工具包 (WDK)](https://docs.microsoft.com/windows-hardware/drivers/download-the-wdk)

- [Windows 符号程序包](debugger-download-symbols.md)  

- [Windows Hardware Lab Kit](https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit)

- [下载并安装 Windows 评估和部署工具包 (Windows ADK)](https://docs.microsoft.com/windows-hardware/get-started/adk-install)

- [Windows 预览体验成员 - Windows 预览版本](https://insider.windows.com/)
