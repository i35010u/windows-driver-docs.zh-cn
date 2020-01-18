---
title: WinDbg 预览-数据模型菜单
description: 本部分介绍如何使用 WinDbg 预览调试器中的 "数据模型" 菜单。
ms.date: 01/10/2020
ms.localizationpriority: medium
ms.openlocfilehash: 4b62daedbcfe0ad45a61211f2b2037009bfbaad7
ms.sourcegitcommit: 6d930ed810124ade8e29a617c7abcd399113696f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/17/2020
ms.locfileid: "76256755"
---
# <a name="windbg-preview---data-model-menu"></a>WinDbg 预览-数据模型菜单

本部分介绍如何使用 WinDbg 预览调试器中的 "数据模型" 菜单。

## <a name="new-model-query"></a>新建模型查询

使用 "新建模型查询" 对话框可以创建新的模型查询。 你可以在此处放置任何内容，并将其放入普通 `dx` 命令。

例如，指定 `Debugger.Sessions` 检查调试器会话对象。 

!["新建数据模型查询" 对话框](images/windbgx-data-model-new-model-dialog.png)

有关调试器对象的常规信息，请参阅[dx （显示调试器对象模型表达式）](dx--display-visualizer-variables-.md)。

使用 LINQ 查询更深入地挖掘会话。 此查询显示运行最多线程的前5个进程。 

```dbgcmd
Debugger.Sessions.First().Processes.Select(p => new { Name = p.Name, ThreadCount = p.Threads.Count() }).OrderByDescending(p => p.ThreadCount),5
```

![数据模型浏览显示进程和线程的窗口](images/windbgx-data-model-process-threads.png)

## <a name="data-model-explorer"></a>数据模型资源管理器

使用数据模型资源管理器可以快速浏览 `Debugger` 命名空间中的每个数据模型对象。

![显示调试对象会话的 "数据模型资源管理器" 窗口](images/windbgx-data-model-explore-window.png)

### <a name="display-mode"></a>显示模式

使用显示模式在网格和层次结构显示模式之间进行切换。 您可以右键单击列标题，以隐藏或显示更多列。

网格模式可用于在对象中进行深化。 例如，下面是网格视图中前面的顶层线程查询。 

![数据模型浏览显示顶部线程的窗口](images/windbgx-data-model-process-threads-grid.png)

单击带下划线的项时，将打开新选项卡，并运行查询以显示该信息。

此查询显示即插即用设备树中的设备，这些设备按用于内核会话的物理设备对象驱动程序的名称进行分组。

```dbgcmd
Debugger.Sessions.First().Devices.DeviceTree.Flatten(n => n.Children).GroupBy(n => n.PhysicalDeviceObject->Driver->DriverName.ToDisplayString()) 
```

![数据模型浏览窗口在网格视图中显示即插即用设备树](images/windbgx-data-model-pnp-device.png)

### <a name="change-query"></a>更改查询

使用 "更改查询" 更改在 "活动数据模型" 窗口中使用的查询。

---

## <a name="see-also"></a>另请参阅

[dx （显示调试器对象模型表达式）](dx--display-visualizer-variables-.md)

[使用 WinDbg Preview 进行调试](debugging-using-windbg-preview.md)
