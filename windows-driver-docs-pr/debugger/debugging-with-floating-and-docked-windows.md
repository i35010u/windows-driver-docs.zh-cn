---
title: 使用浮动和停靠窗口进行调试
description: 使用浮动和停靠窗口进行调试
keywords:
- 停靠窗口，调试
- 浮动窗口，调试
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9cea9e3dde4a7a19db2440f7199fe98df5f777ee
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96785279"
---
# <a name="debugging-with-floating-and-docked-windows"></a>使用浮动和停靠窗口进行调试


## <span id="ddk_debugging_with_floating_and_docked_windows_dbg"></span><span id="DDK_DEBUGGING_WITH_FLOATING_AND_DOCKED_WINDOWS_DBG"></span>


如果窗口浮动、停靠或停靠在选项卡式集合中，则 "调试信息" 窗口中可用的功能不受影响。

### <a name="span-idoverview_of_the_window_configurationspanspan-idoverview_of_the_window_configurationspanoverview-of-the-window-configuration"></a><span id="overview_of_the_window_configuration"></span><span id="OVERVIEW_OF_THE_WINDOW_CONFIGURATION"></span>窗口配置概述

浮动窗口未连接到 WinDbg 窗口或任何其他停靠。 浮动窗口始终直接显示在 WinDbg 窗口之前。

停靠的窗口占据 WinDbg 窗口或单独的停靠中的固定位置。

当两个或多个停靠窗口一起形成选项卡式时，它们将在框架中占用相同的位置。 一次只能查看其中一个选项卡式窗口。 每个选项卡式窗口集合的底部是一组选项卡。 选定的选项卡指示集合中的哪个窗口可见。

### <a name="span-idmaking_a_window_activespanspan-idmaking_a_window_activespanmaking-a-window-active"></a><span id="making_a_window_active"></span><span id="MAKING_A_WINDOW_ACTIVE"></span>使窗口处于活动状态

无论窗口的位置如何，都可以使其处于活动状态。 当浮动窗口处于活动状态时，它会显示在前台。 如果其他停靠中的窗口处于活动状态，则该停靠将显示在前台。 当 WinDbg 窗口内的停靠窗口处于活动状态时，一个或多个浮动窗口可能仍会掩盖停靠窗口。

若要使浮动窗口或停靠窗口处于活动状态，请单击其标题栏。 若要使固定窗口处于活动状态，请单击其选项卡。

还可以通过使用 WinDbg 菜单或工具栏使窗口处于活动状态。 可以通过单击 " **窗口** " 菜单底部的 "窗口名称" 来激活任何窗口。 你还可以通过在 "视图" 菜单上单击 "**视图**" 菜单上的 "名称" 或单击其工具栏按钮，激活除 "[内存" 窗口](memory-window.md)或 ") [源](source-window.md)" 窗口之外的任何窗口 (。

按 CTRL + TAB 在调试信息窗口之间切换。 通过重复按这些键，您可以扫描所有窗口，而不管它们是浮动、停靠还是固定窗口的一部分。 释放 CTRL 键后，当前正在查看的窗口将变为活动状态。

ALT + TAB 快捷键是标准的 Microsoft Windows 快捷键，用于在桌面上的窗口之间进行切换。 你可以使用这些快捷键在 WinDbg 窗口和你已创建的任何其他停靠之间切换。 还可以通过单击 Windows 任务栏中的按钮使其成为活动的。

 

 





