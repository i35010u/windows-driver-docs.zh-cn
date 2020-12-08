---
title: 调整窗口大小和移动窗口
description: 调整窗口大小和移动窗口
keywords:
- 调试信息窗口，调整窗口大小并移动窗口
- 调整大小和移动窗口
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 74af171ef02d4f1ec8feeee64264347ea86625b6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96798359"
---
# <a name="resizing-and-moving-a-window"></a>调整窗口大小和移动窗口


## <span id="ddk_resizing_and_moving_windows_dbg"></span><span id="DDK_RESIZING_AND_MOVING_WINDOWS_DBG"></span>


浮动窗口始终与 WinDbg 窗口关联。 如果最大程度地减少 WinDbg，将最大程度地减少所有浮动窗口。 如果还原 WinDbg，则会还原所有浮动窗口。 永远不能在 WinDbg 窗口的后面放置浮动窗口。

除非已在窗口的快捷菜单中选择了 " **随框架移动** "，否则每个浮动窗口将彼此独立地与它们相互移动。

停靠窗口在 WinDbg 帧内占用固定位置。 如果调整 WinDbg 大小，则所有停靠的窗口都将自动缩放到新的大小。 这种情况同样适用于已停靠在单独的停靠中的窗口。

如果将鼠标指针移动到两个停靠窗口之间的边框，鼠标指针将变为一个箭头。 通过拖动此箭头，您可以调整两个相邻窗口的大小，并使其处于停靠状态。

WinDbg 窗口始终填充停靠窗口。 除非没有停靠窗口，否则窗口中永远不会有任何空白区域。 这种情况同样适用于独立坞。

 

 





