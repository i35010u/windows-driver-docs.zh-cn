---
title: 取消停靠窗口
description: 取消停靠窗口
keywords:
- 调试信息窗口，移除窗口
- 未停靠窗口
- 移除窗口
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: f5b93e6c9aa0732b2016d79e024eebc1fe40492e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803249"
---
# <a name="undocking-a-window"></a>取消停靠窗口


## <span id="ddk_undocking_a_window_dbg"></span><span id="DDK_UNDOCKING_A_WINDOW_DBG"></span>


若要取消停靠窗口并使其成为浮动窗口，请执行下列操作之一：

-   双击窗口的标题栏。

-   打开快捷菜单，方法是：右键单击窗口的标题栏，右键单击该窗口的选项卡（如果它是选项卡式集合的一部分，或单击右上角的窗口图标），然后单击 " **移除**"。

-   在 WinDbg 窗口中的 " **窗口** " 菜单上，单击 " **全部移除**"。 此命令会将所有停靠的窗口更改为浮动窗口。

通过上述方法之一取消停靠窗口时，窗口将返回到它以前的未停靠位置。

还可以通过单击停靠窗口的标题栏拖动该窗口。 此操作可让你将窗口移到其他停靠位置或取消停靠。  (将停靠窗口拖到新位置的工作方式与将浮动窗口拖到新位置完全相同。 有关将浮动窗口拖到新位置的详细信息，请参阅 [停靠窗口](docking-a-window.md)。 ) 

当你尝试按以上任一方法取消停靠或拖动选项卡式窗口时，只会移动选项卡式集合中的活动窗口。

 

 





