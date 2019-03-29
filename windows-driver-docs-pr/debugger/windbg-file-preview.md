---
title: WinDbg 预览版-文件菜单
description: 本部分介绍如何在 WinDbg 预览调试程序中使用文件菜单。
ms.date: 08/04/2017
ms.localizationpriority: medium
ms.openlocfilehash: cba9d8ab2c98735dd78be50bfa78b07e3a979a82
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56562384"
---
# <a name="windbg-preview---file-menu"></a>WinDbg 预览版-文件菜单 

本主题介绍如何使用文件菜单。

### <a name="start-debugging"></a>开始调试

当你首次打开文件菜单时，您将看到*开始调试*和最新的调试器目标。 使用*开始调试*新配置并打开前几个调试器会话。

#### <a name="recent"></a>Recent

最近列表包含你的新工作区和调试器连接的列表。 工作区的工作设置的详细信息请参阅[WinDbg 预览版安装程序-设置和工作区](windbg-setup-preview.md)。

右键单击菜单可用于管理工作区，如固定、 重命名和移动它们。 以及记事本中编辑这些实体。

![工作区文件右键单击打开重命名编辑显示在记事本 pin 菜单并从列表中删除，以及清除已取消固定的目标](images/windbgx-workspace-right-click.png)

#### <a name="start-a-new-session"></a>启动新的会话

使用中的其他选项卡*开始调试*部分以启动新的调试程序会话，连接或启动的进程。 启动新会话的详细信息请参阅[WinDbg 预览的启动模式下的用户会话](windbg-user-mode-preview.md)和[WinDbg 预览版-启动内核模式会话](windbg-kernel-mode-preview.md)


### <a name="save-workspace"></a>保存工作区

使用*保存工作区*保存当前工作区。

会话的连接信息存储在工作区配置文件。 工作区文件都会保存.debugTarget 文件扩展名。 

工作区文件的默认位置为： 

```console
C:\Users\*UserName*\AppData\Local\DBG\targets
```

### <a name="open-source-file"></a>开放源代码文件

使用*开放源代码文件*若要打开的源文件。 如果想要使用的其他源尚未加载由于执行代码的文件执行此操作。 有关如何使用源代码文件的详细信息，请参阅[在 WinDbg 中源代码调试](source-window.md)


### <a name="open-script"></a>打开脚本

使用*打开脚本*若要打开现有的 Javascript 或 NatVis 脚本。 有关使用脚本的详细信息请参阅[WinDbg 预览版-脚本菜单](windbg-scripting-preview.md)。

### <a name="settings"></a>设置

使用设置菜单来设置源和符号路径，以及为调试器选择浅色和深色主题。 有关详细信息设置，请参阅[WinDbg 预览版安装程序-设置和工作区](windbg-setup-preview.md)。


### <a name="about"></a>关于
使用*有关*要显示调试程序的生成版本信息。 您可以使用也使用此屏幕可以查看 Microsoft 隐私声明。

---
 
## <a name="see-also"></a>请参阅

[调试使用 WinDbg 预览](debugging-using-windbg-preview.md)
 





