---
title: 创建和打开工作区
description: 创建和打开工作区
keywords:
- 工作区，创建
- 工作区，打开
- 工作区，命名工作区
- 工作区，默认工作区
- 工作区，工作区类型
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: db7f13b7ae11c447d9c97e1ce404ab8527fde89d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96811213"
---
# <a name="creating-and-opening-a-workspace"></a>创建和打开工作区


## <span id="ddk_creating_and_opening_a_workspace_dbg"></span><span id="DDK_CREATING_AND_OPENING_A_WORKSPACE_DBG"></span>


WinDbg 具有两种工作区： *默认工作区* 和 *命名工作区*。

### <a name="span-iddefault_workspacesspanspan-iddefault_workspacesspandefault-workspaces"></a><span id="default_workspaces"></span><span id="DEFAULT_WORKSPACES"></span>默认工作区

WinDbg 具有几种不同类型的默认工作区：

-   当 WinDbg 处于休眠状态时，使用 *基本工作区* 。

-   使用 **-p**[**命令行选项**](windbg-command-line-options.md)或使用文件连接到用户模式进程时，将使用 *默认用户模式工作区* ([|附加到进程](file---attach-to-a-process.md)命令) 。

-   当你连接到调试服务器时，将使用 *远程默认工作区* 。

-   当 WinDbg 开始内核模式调试会话时，将使用 *默认的内核模式工作区* 。

-   在 WinDbg 附加到目标计算机之后，在内核模式调试过程中将使用 *特定于处理器的工作区* 。 基于 x86 和基于 x64 的处理器有单独的特定于处理器的工作区。

当 WinDbg 创建用于调试的用户模式进程时，将为该可执行文件创建一个工作区。 每个创建的可执行文件都有自己的工作区。

当 WinDbg 分析转储文件时，将为该转储文件分析会话创建一个工作区。 每个转储文件都有自己的工作区。

当你开始调试会话时，将加载相应的工作区。 结束调试会话或退出 WinDbg 时，会显示一个对话框，询问你是否要保存对当前工作区所做的更改。 如果用 **-QY**[**命令行选项**](windbg-command-line-options.md)启动 WinDbg，则不会出现此对话框，并且会自动保存工作区。 此外，如果通过 **-Q** 命令行选项启动 WinDbg，则不会出现此对话框，并且不会保存任何更改。

以累计方式加载工作区。 始终首先加载基本工作区。 当你开始特定的调试操作时，将加载相应的工作区。 因此，大多数调试都是在加载了两个工作区之后完成的。 内核模式调试在 (基本工作区、默认的内核模式工作区和特定于处理器的工作区) 加载三个工作区之后完成。

为了获得最高的效率，如果要将设置应用于所有 WinDbg 工作，则应将其保存在较低级别的工作区中。

**注意**   调试信息窗口的布局是工作区的累积行为中的一个例外。 每个窗口的位置、停靠状态和大小仅由您打开的最新工作区决定。 此行为包括监视窗口的内容以及您在每个 [内存窗口](memory-window.md)中查看的位置。 打开新的工作区时，不会清除 [调试器命令窗口](debugger-command-window.md) 中的命令历史记录，但会重置所有其他窗口状态。

 

若要访问基本工作区，请启动没有目标的 WinDbg，或在会话完成后单击 "**调试**" 菜单上的 "[停止调试](debug---stop-debugging.md)"。 然后，你可以在基本工作区中进行任何所需的编辑。

### <a name="span-idnamed_workspacesspanspan-idnamed_workspacesspannamed-workspaces"></a><span id="named_workspaces"></span><span id="NAMED_WORKSPACES"></span>命名工作区

你还可以指定工作区名称，然后单独保存或加载它们。 加载命名工作区后，将禁用默认工作区的所有自动加载和保存。

命名工作区包含默认工作区不包含的一些其他信息。 有关此附加信息的详细信息，请参阅 [工作区内容](workspace-contents.md)。

### <a name="span-idopening__saving__and_clearing_workspacesspanspan-idopening__saving__and_clearing_workspacesspanopening-saving-and-clearing-workspaces"></a><span id="opening__saving__and_clearing_workspaces"></span><span id="OPENING__SAVING__AND_CLEARING_WORKSPACES"></span>打开、保存和清除工作区

若要控制工作区，你可以执行以下操作：

-   使用 **-W** [**命令行选项**](windbg-command-line-options.md)打开并加载命名的工作区。

-   使用 **-WF** [**命令行选项**](windbg-command-line-options.md)打开并加载文件中的工作区。

-   使用 **-WX** [**命令行选项**](windbg-command-line-options.md)禁用所有自动工作区加载。 只有显式工作区命令会导致保存或加载工作区。

-   通过单击 "**文件**" 菜单上的 "[打开工作区](file---open-workspace.md)" 或按 CTRL + W 打开并加载命名的工作区。

-   单击 "**文件**" 菜单上的 "[保存工作区](file---save-workspace.md)"，保存当前的默认工作区或当前命名的工作区。

-   为当前工作区指定一个名称，并通过在 "**文件**" 菜单上单击 "[保存工作区](file---save-workspace-as.md)" 将其保存。

-   通过单击 "**文件**" 菜单上的 "[清除工作区](file---clear-workspace.md)"，从当前工作区中删除特定项和设置。

-   通过单击 "**文件**" 菜单上的 "[删除工作区](file---delete-workspaces.md)" 删除工作区。

-   在 "**文件**" 菜单上单击 "文件"[中的 "打开工作区](file---open-workspace-in-file.md)"，从文件中打开并加载工作区。

-   单击 "**文件**" 菜单上的 "[将工作区保存到文件](file---save-workspace-to-file.md)"，将工作区保存到文件。

 

 





