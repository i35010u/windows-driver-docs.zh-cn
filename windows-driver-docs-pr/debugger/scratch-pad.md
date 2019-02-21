---
title: 使用暂存器
description: 使用暂存器
ms.assetid: a0f6ce9c-7fad-4df6-bad8-0ea1bc5bfc52
keywords:
- 调试信息窗口中，暂存器
- 草稿板
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: f96ffc118e1fa01dc633ab4175c4f859944bb7f4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525929"
---
# <a name="using-the-scratch-pad"></a>使用暂存器


## <span id="ddk_scratch_pad_dbg"></span><span id="DDK_SCRATCH_PAD_DBG"></span>


草稿板窗口是在其可以键入，然后将文本保存剪贴板。

### <a name="span-idopeningthescratchpadwindowspanspan-idopeningthescratchpadwindowspanopening-the-scratch-pad-window"></a><span id="opening_the_scratch_pad_window"></span><span id="OPENING_THE_SCRATCH_PAD_WINDOW"></span>打开草稿板窗口

若要打开或切换到草稿板窗口在 WinDbg 窗口中，在**视图**菜单上，单击**草稿板**。 (还可以按 ALT + 8，或单击**草稿板 (Alt + 8)** 按钮 (![的草稿板按钮的屏幕截图](images/tbspad.png)) 工具栏上。)

下面的屏幕截图显示了草稿板窗口的一个示例。

![草稿板窗口的屏幕截图](images/window-scratchpad.png)

### <a name="span-idusingthescratchpadwindowspanspan-idusingthescratchpadwindowspanusing-the-scratch-pad-window"></a><span id="using_the_scratch_pad_window"></span><span id="USING_THE_SCRATCH_PAD_WINDOW"></span>使用草稿板窗口

在草稿板窗口中，可以执行以下操作：

-   若要在草稿板窗口中键入，单击你想要添加的文本，然后开始键入的窗口。 此外可以使用标准复制和粘贴功能。 草稿板窗口的内容不会影响调试器的操作。 此窗口存在只是为了帮助进行文本编辑。

-   如果关闭草稿板窗口中，文本会保留，并重新打开该窗口时可用。 此外可以通过使用文件关联来保存暂存器窗口中的文本。

草稿板窗口具有带其他命令的快捷方式菜单。 若要访问菜单，请右键单击标题栏或单击窗口 （在右上角附近的图标![显示的草稿板窗口工具栏快捷方式菜单按钮的屏幕截图](images/tbspad.png))。 此菜单包含以下命令：

-   （仅限菜单）**将与文件相关联**打开一个对话框，可以通过它选择一个文本文件。 选择文件后，在草稿板中的当前文本被清除，并且替换为所选文件中的文本。 与此文件关联暂存器时，所有新文本键入到暂存器保存到文件。 可以结束与文件关联，或者通过选择**结束文件关联**快捷方式菜单选项或通过关闭并重新打开便笺。

-   （仅限菜单）**结束文件关联**结束与指定的文本文件的暂存器关联。 便笺中的所有文本，在选择此选项之前先都保存在文件中。 在中键入的所有文本便笺关联结束后不再保存在文本文件中。

-   **停靠**或**取消停靠**将使窗口进入或离开停靠的状态。

-   （仅限菜单）**移到新停靠**关闭便笺并将其打开新的平台中。

-   （仅限菜单）**设置为选项卡形式停靠为窗口中，键入目标**的暂存器不可用。 此选项才可供[源](source-window.md)或[内存](memory-window.md)windows。

-   **始终浮点**将使窗口停靠，即使仍拖到停靠位置。

-   **移动与帧**将使窗口移动时移动的 WinDbg 帧，即使在窗口已解除固定。 停靠和浮动的选项卡式，windows 的详细信息，请参阅[定位 Windows](positioning-the-windows.md)。

-   **帮助**有关 Windows 调试工具文档中打开此主题。

-   **关闭**关闭此窗口。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

停靠和浮动的选项卡式，windows 的详细信息，请参阅[定位 Windows](positioning-the-windows.md)。 有关可以使用来控制调试信息 windows 的所有技术的详细信息，请参阅[使用调试信息 Windows](using-debugging-information-windows.md)。

 

 





