---
title: 自定义主题
description: 自定义主题
keywords:
- 主题，自定义
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 245d6745434e9aa05bc96fa73b3826199407a13e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96786969"
---
# <a name="customizing-a-theme"></a>自定义主题


## <span id="ddk_creating_and_opening_a_workspace_dbg"></span><span id="DDK_CREATING_AND_OPENING_A_WORKSPACE_DBG"></span>


自定义主题之前，必须先加载该主题。 有关详细信息，请参阅 [加载主题](loading-a-theme.md) 。

加载主题后，启动不带命令行参数的 WinDbg。 这将打开 "基本" 工作区。 自定义主题有两个常见领域：设置路径和调整窗口位置。

完成任何所需的调整后，请退出 WinDbg 并通过从 "**文件**" 菜单中选择 "**保存工作区**" 来保存工作区。 若要将新设置保存到 .reg 文件，请打开 Regedit，并将 **HKCU \\ Software \\ Microsoft \\ Windbg \\ 工作区** 下的注册表项导出到 .reg 文件中。

### <a name="span-idsetting_pathsspanspan-idsetting_pathsspansetting-paths"></a><span id="setting_paths"></span><span id="SETTING_PATHS"></span>设置路径

通过设置适当的路径，可以确保 WinDbg 能找到需要有效调试的所有文件。 要设置三个主要路径：符号路径、源路径和可执行图像路径。

下面是如何设置符号和源路径的示例。 可执行映像路径通常与符号路径相同。

设置符号路径：

```text
SRV*c:\MySymCache*\\CompanySymbolServer\Symbols;SRV*c:\WinSymCache*https://msdl.microsoft.com/download/symbols
```

设置源路径：

```text
SRV*;d:\MySourceRoot
```

### <a name="span-idadjusting_window_positionspanspan-idadjusting_window_positionspanadjusting-window-position"></a><span id="adjusting_window_position"></span><span id="ADJUSTING_WINDOW_POSITION"></span>调整窗口位置

使用主题之前，应调整窗口定位，使 WinDbg 正确处理源文件。 这可确保源窗口知道停靠位置。

首先，在 WinDbg 中打开源窗口。 选项卡-将此窗口停靠在源窗口旁的占位符上。 为了使建立正确的关系，占位符窗口必须是停靠的最上方窗口，然后才能执行此选项卡停靠操作。 现在关闭源窗口，而不是占位符窗口。

由于调试信息 windows "请记住" 其最后一个停靠操作，因此在执行此过程后，每个源窗口的上次停靠操作都与其中一个占位符窗口关联。 由于此内存属性，不应关闭任何占位符窗口。 此外，如果选择更改主题的配置，则在停靠中重新定位的任何窗口都应始终使用占位符文件停靠。

使用以下操作创建了适用于 Windows 的调试工具附带的示例主题：

将占位符 \* .c 文件放入停靠中。

选项卡-将每个窗口类型停靠在所需占位符窗口之上。

有关在 WinDbg 中调整窗口位置的详细信息，请参阅 [定位窗口](positioning-the-windows.md)。

 

 





