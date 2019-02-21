---
title: 自定义主题
description: 自定义主题
ms.assetid: 3dddbf19-34ec-4cb0-b427-854ae7622fa1
keywords:
- 自定义主题
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: c0bf54b37d4ac1e7941f83276a8744c93b8e7e15
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541391"
---
# <a name="customizing-a-theme"></a>自定义主题


## <span id="ddk_creating_and_opening_a_workspace_dbg"></span><span id="DDK_CREATING_AND_OPENING_A_WORKSPACE_DBG"></span>


在自定义主题之前, 必须先加载它。 请参阅[加载主题](loading-a-theme.md)有关详细信息。

加载主题后，启动 WinDbg 不带任何命令行参数。 这将打开基本工作区。 有两个常见方面的自定义主题的重点： 设置路径和调整窗口的位置。

任何想要完成后调整，退出 WinDbg，并通过选择保存你的工作区**保存工作区**从**文件**菜单。 如果你想要将新的设置保存到.reg 文件，打开注册表编辑器，并将导出下的注册表项**HKCU\\软件\\Microsoft\\Windbg\\工作区**.reg 文件。

### <a name="span-idsettingpathsspanspan-idsettingpathsspansetting-paths"></a><span id="setting_paths"></span><span id="SETTING_PATHS"></span>设置路径

通过设置相应的路径，可以确保 WinDbg 可以找到的所有文件，它需要有效地调试。 有三个设置的主要方式： 符号路径、 源路径和可执行映像路径。

以下是有关如何设置符号和源路径的示例。 可执行映像路径通常是与你的符号路径相同。

若要设置符号路径：

```text
SRV*c:\MySymCache*\\CompanySymbolServer\Symbols;SRV*c:\WinSymCache*https://msdl.microsoft.com/download/symbols
```

若要设置您的源路径：

```text
SRV*;d:\MySourceRoot
```

### <a name="span-idadjustingwindowpositionspanspan-idadjustingwindowpositionspanadjusting-window-position"></a><span id="adjusting_window_position"></span><span id="ADJUSTING_WINDOW_POSITION"></span>调整窗口位置

在使用之前您的主题，应调整窗口定位，以便 WinDbg 正确处理源代码文件。 这可确保源 windows 知道停靠的位置。

首先在 WinDbg 中打开源窗口。 选项卡形式停靠此窗口与设置保留在源窗口的占位符。 按正确的关系进行顺序，占位符窗口停靠面板中最上面的窗口之前必须执行此选项卡停靠的操作。 现在，关闭源窗口中，但不是占位符窗口。

调试 windows"记住"停靠其最后一次操作的信息，因为每个源窗口中的最后一个停靠操作是与一个占位符 windows 相关联之后执行此过程。 由于有此内存属性，您不应关闭任何占位符的窗口。 此外，如果您选择要更改的主题配置，在平台中重新定位任何窗口应始终为停靠选项卡-在一起的占位符文件。

调试工具的 Windows 中包含的示例主题创建使用以下操作：

放置和定位占位符\*.c 文件到停靠。

选项卡形式停靠在所需的占位符窗口上每个窗口类型。

有关调整窗口在 WinDbg 中的位置的进一步信息，请参阅[定位 Windows](positioning-the-windows.md)。

 

 





