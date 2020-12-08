---
title: 排列窗口
description: 排列窗口
keywords:
- 调试信息窗口，停靠建议
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 986daee15cc63e07064966551bd44477fd3cdee4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96819311"
---
# <a name="arranging-windows"></a>排列窗口


## <span id="ddk_suggested_configurations_dbg"></span><span id="DDK_SUGGESTED_CONFIGURATIONS_DBG"></span>


一个有用的窗口排列是将所有 [源窗口](source-window.md) 合并为一个选项卡式集合。 要执行此操作，最简单的方法是通过在源窗口的快捷菜单中选择 " **设置为窗口类型的 tab 停靠目标** " 选项，将第一个源窗口标记为所有源窗口的选项卡停靠目标。 完成此操作后，以后打开的所有源窗口都将自动包含在具有此第一个源窗口的选项卡式集合中。 当窗口为时，将不会关闭标记为选项卡停靠目标的源窗口 **|选择 "关闭所有源窗口** " 菜单命令。 因此，您可以为源窗口设置一个占位符窗口，该窗口仅在您需要时才会关闭。

此集合可以占据 WinDbg 窗口的一半，也可以将其放在单独的停靠中。

如果希望每个调试信息窗口完全分离，则可以为每个窗口创建一个停靠。 这种安排使你可以最小化或最大化每个窗口。

如果希望所有窗口浮动，应在每个窗口的快捷菜单上选择 " **始终浮动** "，以便可以将每个窗口单独拖到任何位置。

或者，可以使用 "**窗口**" 菜单上的 " [MDI 模拟](window---mdi-emulation.md)" 命令。 此命令将生成所有 windows 浮动窗口，并在框架窗口中对其进行限制。 此行为在引入停靠模式之前模拟 WinDbg 的行为。

如果使用的是双监视器，则可以将 WinDbg 窗口放在一个监视器中，将一个额外的停靠在另一个监视器中。

适用于各种调试方案的一些标准窗口布局包含在 Windows 的调试工具包中。 有关这些安排的详细信息，请参阅 [使用和自定义 WinDbg 主题](using-and-customizing-windbg-themes.md)。

 

 





