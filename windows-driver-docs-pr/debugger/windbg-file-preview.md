---
title: WinDbg 预览-"文件" 菜单
description: 本部分介绍如何使用 WinDbg 预览调试器中的 "文件" 菜单。
ms.date: 01/10/2020
ms.localizationpriority: medium
ms.openlocfilehash: e5e4e33e13ea8de20f8b6fb04a0dbf3f7cb9c496
ms.sourcegitcommit: 6d930ed810124ade8e29a617c7abcd399113696f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/17/2020
ms.locfileid: "76256752"
---
# <a name="windbg-preview---file-menu"></a>WinDbg 预览-"文件" 菜单

![带有位模式的 windbg 预览的小徽标](images/windbgx-preview-logo.png)

本主题介绍如何使用 "文件" 菜单。

### <a name="start-debugging"></a>“启动调试”

当你首次打开 "文件" 菜单时，你将看到 "*启动调试*" 和最近使用的调试器目标。 使用 "*启动调试*" 配置新的和打开的以前的调试器会话。

#### <a name="recent"></a>最近使用的项目

"最近" 列表包含最近使用的工作区和调试器连接的列表。 有关工作设置工作区的详细信息，请参阅[WinDbg 预览设置–设置和工作区](windbg-setup-preview.md)。

您可以使用右键单击菜单来管理工作区，例如固定、重命名和移动工作区。 并在记事本中进行编辑。

![工作区文件右键单击菜单，显示 "在记事本中打开重命名" "pin" 和 "从列表中删除"，以及清除取消固定目标](images/windbgx-workspace-right-click.png)

#### <a name="start-a-new-session"></a>启动新会话

使用 "*启动调试*" 部分中的 "其他" 选项卡可启动新的调试器会话，例如附加或启动进程。 有关启动新会话的详细信息，请参阅[Windbg preview-启动用户模式会话](windbg-user-mode-preview.md)和[WinDbg preview-启动内核模式会话](windbg-kernel-mode-preview.md)

### <a name="save-workspace"></a>保存工作区

使用 "*保存工作区*" 保存当前工作区。

会话连接信息存储在工作区配置文件中。 工作区文件以 debugTarget 文件扩展名存储。

工作区文件的默认位置为：

```console
C:\Users\*UserName*\AppData\Local\DBG\targets
```

### <a name="open-source-file"></a>打开源文件

使用 "*打开源文件*" 打开源文件。 如果要使用因代码执行而未加载的其他源文件，请执行此操作。 有关使用源文件的详细信息，请参阅[WinDbg 中的源代码调试](source-window.md)

### <a name="open-script"></a>打开脚本

使用 "*打开脚本*" 打开现有 Javascript 或 NatVis 脚本。 有关使用脚本的详细信息，请参阅[WinDbg 预览-脚本菜单](windbg-scripting-preview.md)。

### <a name="settings"></a>“设置”

使用 "设置" 菜单可设置源和符号路径，以及选择调试器的浅色和深色主题。 有关设置的详细信息，请参阅[WinDbg 预览设置-设置和工作区](windbg-setup-preview.md)。

### <a name="about"></a>关于

使用 "*关于*" 显示调试器的生成版本信息。 你还可以使用此屏幕查看 Microsoft 隐私声明。

### <a name="exit"></a>退出

使用*exit*退出调试器。

---

## <a name="see-also"></a>另请参阅

[使用 WinDbg Preview 进行调试](debugging-using-windbg-preview.md)
