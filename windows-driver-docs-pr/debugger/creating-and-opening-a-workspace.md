---
title: 创建和打开工作区
description: 创建和打开工作区
ms.assetid: 0163f380-f982-4635-a450-ed83f0b52e03
keywords:
- 工作区创建
- 打开的工作区
- 工作区，名为工作区
- 默认工作区的工作区
- 工作区类型的工作区
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 11cd78591bfa934f4ac7f7ee7dcb2760d6641b70
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542636"
---
# <a name="creating-and-opening-a-workspace"></a>创建和打开工作区


## <span id="ddk_creating_and_opening_a_workspace_dbg"></span><span id="DDK_CREATING_AND_OPENING_A_WORKSPACE_DBG"></span>


WinDbg 有两种类型的工作区：*默认工作区*并*名为工作区*。

### <a name="span-iddefaultworkspacesspanspan-iddefaultworkspacesspandefault-workspaces"></a><span id="default_workspaces"></span><span id="DEFAULT_WORKSPACES"></span>默认工作区

WinDbg 具有几种不同的默认工作区：

-   *基工作区*WinDbg 处于休眠状态时使用。

-   *默认用户模式下工作区*附加到用户模式进程时使用 (通过使用 **-p**[**命令行选项**](windbg-command-line-options.md)或使用[文件 |附加到进程](file---attach-to-a-process.md)命令)。

-   *远程默认工作区*连接到调试服务器时使用。

-   *默认内核模式下工作区*WinDbg 开始内核模式调试会话时使用。

-   *特定于处理器的工作区*内核模式调试后 WinDbg 附加到目标计算机期间使用。 有单独的特定于处理器的工作区的基于 x86 和基于 x64 的处理器。

当 WinDbg 创建用户模式进程进行调试时，为该可执行文件创建一个工作区。 每个创建的可执行文件具有自己的工作区。

WinDbg 分析转储文件时为该转储文件分析会话创建一个工作区。 每个转储文件包含其自己的工作区。

当您开始调试会话时，加载相应的工作区。 当调试会话结束或退出 WinDbg 时，对话框会显示，并询问您是否要保存对当前工作区所做的更改。 如果启动的 WinDbg **-QY**[**命令行选项**](windbg-command-line-options.md)，不会显示此对话框中，并自动保存工作区。 此外，如果启动的 WinDbg **-Q**命令行选项不会显示此对话框中，并不保存任何更改。

累积方式加载工作区。 始终首先加载的基本工作区。 当特定的调试操作开始时，将加载相应的工作区。 因此在加载完两个工作区后，完成大多数调试。 内核模式调试被完成后 （基本工作区中，默认内核模式下工作区中和特定于处理器的工作区） 已加载三个工作区。

为最高的效率，应在较低级别工作区中保存设置如果想要应用于所有 WinDbg 工作。

**请注意**  调试的信息窗口的布局是累积的行为的工作区的一个例外。 仅在打开的最新工作区由确定位置、 停靠状态和每个窗口的大小。 此行为包括监视窗口查看每个位置的内容[内存窗口](memory-window.md)。 中的命令历史记录[调试器命令窗口](debugger-command-window.md)时打开新的工作区，但所有其他窗口状态将重置将不被清除。

 

若要访问的基本工作区，请启动 WinDbg 时没有目标，或单击[停止调试](debug---stop-debugging.md)上**调试**菜单在会话完成后。 然后可以允许在基本的工作区中的任何编辑。

### <a name="span-idnamedworkspacesspanspan-idnamedworkspacesspannamed-workspaces"></a><span id="named_workspaces"></span><span id="NAMED_WORKSPACES"></span>命名工作区

此外可以提供工作区的名称，然后保存或单独加载它们。 加载指定的工作区后，禁用所有自动加载和保存默认工作区。

命名工作区包含默认工作区不这样做一些其他信息。 有关此附加信息的详细信息，请参阅[工作区内容](workspace-contents.md)。

### <a name="span-idopeningsavingandclearingworkspacesspanspan-idopeningsavingandclearingworkspacesspanopening-saving-and-clearing-workspaces"></a><span id="opening__saving__and_clearing_workspaces"></span><span id="OPENING__SAVING__AND_CLEARING_WORKSPACES"></span>打开、 保存和清除工作区

若要控制工作区，请执行以下操作：

-   打开，并通过加载指定的工作区 **-W** [**命令行选项**](windbg-command-line-options.md)。

-   打开并使用从文件加载工作区 **-WF** [**命令行选项**](windbg-command-line-options.md)。

-   禁用所有自动使用加载的工作区 **-WX** [**命令行选项**](windbg-command-line-options.md)。 只有显式工作区命令会导致要保存或加载的工作区。

-   打开，并通过单击加载指定的工作区[打开工作区](file---open-workspace.md)上**文件**菜单或按 CTRL + W。

-   通过单击来保存当前的默认工作区或当前命名工作区[保存工作区](file---save-workspace.md)上**文件**菜单。

-   为当前工作区分配一个名称并将其保存通过单击[工作区另存为](file---save-workspace-as.md)上**文件**菜单。

-   从当前工作区中删除特定项和设置，通过单击[清除工作区](file---clear-workspace.md)上**文件**菜单。

-   通过单击删除工作区[删除工作区](file---delete-workspaces.md)上**文件**菜单。

-   打开，并通过单击从文件加载工作区[文件中打开工作区](file---open-workspace-in-file.md)上**文件**菜单。

-   通过单击保存到文件的工作区[保存到文件的工作区](file---save-workspace-to-file.md)上**文件**菜单。

 

 





