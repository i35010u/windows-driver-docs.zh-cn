---
title: 排列 Windows
description: 排列 Windows
ms.assetid: f6c0b778-42a8-4073-8cdb-c4b801e59274
keywords:
- 调试信息窗口中，停靠的建议
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: f2fcc6682e4aefeb87675a6a14e24f5c69f8f9e5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547386"
---
# <a name="arranging-windows"></a>排列 Windows


## <span id="ddk_suggested_configurations_dbg"></span><span id="DDK_SUGGESTED_CONFIGURATIONS_DBG"></span>


一种有用的窗口排列方式是将合并所有你[源 windows](source-window.md)成了一个选项卡式集合。 若要执行此操作的最简单方法是通过选择将在第一个源窗口标记为针对所有源窗口的选项卡形式停靠**设置为选项卡形式停靠为窗口中，键入目标**源窗口的快捷方式菜单中的选项。 完成此操作后，打开的所有将来的源窗口将自动包含在此第一个源范围的选项卡式集合中。 源窗口中标记为选项卡形式停靠时，不会关闭目标**窗口 |关闭所有源 Windows**选择菜单命令。 因此，您可以设置时希望其成为将仅关闭在源窗口的占位符窗口。

此集合可以占用的 WinDbg 窗口下半部分，也可以将它放在单独的停靠。

如果你想要完全独立每个调试信息窗口，可以创建一个停靠为每个窗口。 这种排列方式，可最大程度减少或单独为每个窗口最大化。

如果想要所有 windows 以浮点值，则应选择**始终浮点**每个窗口的快捷菜单上，以便每个窗口拖到任何位置的独立。

或者，可以使用[MDI 仿真](window---mdi-emulation.md)命令**窗口**菜单。 此命令使所有浮动窗口的窗口，并限制在框架窗口内。 此行为来模拟的 WinDbg 的停靠模式引入之前的行为。

使用双监视器时，您可以将 WinDbg 窗口放在一个监视器，并在其他额外停靠。

有关 Windows 调试工具软件包中包含各种调试方案一些标准的窗口排列方式。 有关这些排列方式的详细信息，请参阅[使用和自定义 WinDbg 主题](using-and-customizing-windbg-themes.md)。

 

 





