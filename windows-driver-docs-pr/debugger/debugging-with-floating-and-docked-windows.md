---
title: 使用浮动和停靠窗口进行调试
description: 使用浮动和停靠窗口进行调试
ms.assetid: 2b3e67de-576e-4cbb-bdf1-58a31cea733c
keywords:
- 停靠窗口调试
- 浮动窗口调试
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: c10cec55e56e5e4bfbe3a68033813b11e86faa6d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63346310"
---
# <a name="debugging-with-floating-and-docked-windows"></a>使用浮动和停靠窗口进行调试


## <span id="ddk_debugging_with_floating_and_docked_windows_dbg"></span><span id="DDK_DEBUGGING_WITH_FLOATING_AND_DOCKED_WINDOWS_DBG"></span>


在调试的信息窗口中可用的功能不受影响的窗口是否浮动、 停靠，或停靠选项卡式的集合中。

### <a name="span-idoverviewofthewindowconfigurationspanspan-idoverviewofthewindowconfigurationspanoverview-of-the-window-configuration"></a><span id="overview_of_the_window_configuration"></span><span id="OVERVIEW_OF_THE_WINDOW_CONFIGURATION"></span>窗口配置的概述

未连接到 WinDbg 窗口或任何其他停靠浮动窗口。 浮动窗口始终显示直接放在 WinDbg 窗口。

停靠的窗口 WinDbg 窗口或通过在单独的停靠中占用的固定的位置。

当两个或多个停靠的窗口一起选项卡式时，它们将占用在框架内的同一位置。 您可以一次看到这些选项卡式窗口之一。 在每个选项卡式窗口的底部集合是一组选项卡。 选定的选项卡指示集合中的窗口可见。

### <a name="span-idmakingawindowactivespanspan-idmakingawindowactivespanmaking-a-window-active"></a><span id="making_a_window_active"></span><span id="MAKING_A_WINDOW_ACTIVE"></span>使窗口处于活动状态

可以任何窗口处于活动状态，而不考虑其位置。 浮动窗口处于活动状态，它将显示在前景中。 在其他停靠窗口处于活动状态，该停靠会显示在前台。 WinDbg 窗口中的固定的窗口处于活动状态，当一个或多个浮动窗口仍可能掩盖停靠的窗口。

若要使浮动窗口或停靠的窗口处于活动状态，请单击其标题栏。 若要使选项卡式的集合中的停靠的窗口处于活动状态，请单击其选项卡。

此外可以使使用 WinDbg 菜单或工具栏处于活动状态窗口。 可以通过单击底部的窗口名称激活任何窗口**窗口**菜单。 您还可以激活任何窗口 (而不[内存窗口](memory-window.md)或[源窗口](source-window.md)) 通过单击其名称**视图**菜单或单击工具栏按钮。

按 CTRL + TAB 调试信息窗口之间进行切换。 通过重复按这些密钥，你可以扫描通过的所有窗口，而不考虑是否浮动、 停靠本身，或选项卡式停靠窗口的集合的一部分。 在您发布了 CTRL 键，当前正在查看的窗口将变为活动状态。

ALT + TAB 键盘快捷方式是标准 Microsoft Windows 键盘快捷方式在桌面上窗口之间进行切换。 可以使用这些快捷键 WinDbg 窗口和已创建任何其他停靠之间进行切换。 此外可以使通过单击 Windows 任务栏中的其按钮处于活动状态的停靠。

 

 





