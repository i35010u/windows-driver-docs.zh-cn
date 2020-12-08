---
title: 使用暂存器
description: 使用暂存器
keywords:
- 调试信息窗口，草稿板
- 暂存板
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: cdea5adf28d96c1d7728af35d2a68d7f08515e9f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96830239"
---
# <a name="using-the-scratch-pad"></a>使用暂存器


## <span id="ddk_scratch_pad_dbg"></span><span id="DDK_SCRATCH_PAD_DBG"></span>


"暂存板" 窗口是一个剪贴板，可在其中键入并保存文本。

### <a name="span-idopening_the_scratch_pad_windowspanspan-idopening_the_scratch_pad_windowspanopening-the-scratch-pad-window"></a><span id="opening_the_scratch_pad_window"></span><span id="OPENING_THE_SCRATCH_PAD_WINDOW"></span>打开 "暂存板" 窗口

若要打开或切换到 "暂存板" 窗口，请在 "WinDbg" 窗口的 " **视图** " 菜单上，单击 " **暂存板**"。  (你还可以按 ALT + 8，或单击 **(alt + 8)** 按钮 (![ 工具栏上的 "暂存板" 按钮) 的屏幕截图 ](images/tbspad.png) 。 ) 

以下屏幕截图显示了一个 "暂存板" 窗口的示例。

!["暂存板" 窗口的屏幕截图](images/window-scratchpad.png)

### <a name="span-idusing_the_scratch_pad_windowspanspan-idusing_the_scratch_pad_windowspanusing-the-scratch-pad-window"></a><span id="using_the_scratch_pad_window"></span><span id="USING_THE_SCRATCH_PAD_WINDOW"></span>使用 "暂存板" 窗口

在 "暂存板" 窗口中，你可以执行以下操作：

-   若要在 "暂存面板" 窗口中键入，请在要添加文本的窗口中单击，然后开始键入。 你还可以使用标准的复制和粘贴功能。 "暂存板" 窗口的内容不会影响调试器的操作。 此窗口仅用于帮助进行文本编辑。

-   如果关闭 "暂存板" 窗口，您的文本将被保留，并在重新打开窗口时可用。 还可以通过将文本与文件关联来保存 "暂存板" 窗口中的文本。

"暂存板" 窗口有一个快捷菜单，其中包含其他命令。 若要访问菜单，请右键单击标题栏或单击窗口右上角附近的图标 (![显示 "暂存板" 窗口工具栏快捷菜单的按钮屏幕截图](images/tbspad.png)). 此菜单包含以下命令：

-    (菜单 "仅) **与文件关联** " 会打开一个对话框，通过该对话框可以选择文本文件。 选择该文件后，将清除暂存板中的当前文本，并将其替换为所选文件中的文本。 虽然暂存板与此文件相关联，但键入到草稿板中的所有新文本都将保存到文件中。 可以通过选择 " **结束文件关联** " 快捷菜单选项或关闭并重新打开暂存板来结束与该文件的关联。

-   仅 (菜单) **结束文件关联** 结束与指定文本文件的 "暂存板" 关联。 在选择此选项之前，草稿板中的所有文本都保存在文件中。 关联结束后，在 "暂存" 框中键入的所有文本都不再保存在文本文件中。

-   **停靠** 或 **取消停靠将导致窗口** 进入或离开停靠状态。

-   仅 (菜单) **移动到新的 dock** 会关闭暂存板，并在新的停靠中打开它。

-   仅 (菜单) **"设置为" 窗口类型的选项卡停靠目标对于 "** 草稿板" 不可用。 此选项仅适用于 [源](source-window.md) 或 [内存](memory-window.md) 窗口。

-   **始终浮动** 会导致窗口保持未停靠，即使将其拖动到停靠位置。

-   "**移动到帧**" 会导致在移动 WinDbg 帧时窗口移动，即使窗口未停靠也是如此。 有关停靠窗口、选项卡式窗口和浮动窗口的详细信息，请参阅 [定位窗口](positioning-the-windows.md)。

-   **帮助** 在 Windows 调试工具文档中打开此主题。

-   **关闭** 关闭此窗口。

### <a name="span-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关停靠窗口、选项卡式窗口和浮动窗口的详细信息，请参阅 [定位窗口](positioning-the-windows.md)。 有关可用于控制调试信息窗口的所有方法的详细信息，请参阅 [使用调试信息窗口](using-debugging-information-windows.md)。

 

 





