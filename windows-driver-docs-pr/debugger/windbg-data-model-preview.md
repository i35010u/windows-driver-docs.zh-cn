---
title: WinDbg 预览版-数据模型
description: 本部分介绍如何使用 WinDbg 预览调试器中数据模型菜单。
ms.date: 10/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: d0e35ba5ffb7fa8bd170b1401e3e6b4a80987174
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63353089"
---
# <a name="windbg-preview---data-model"></a>WinDbg 预览版-数据模型 

本部分介绍如何使用 WinDbg 预览调试器中数据模型菜单。

![在调试器中的数据模型菜单的屏幕截图](images/windbgx-data-model-menu.png)


## <a name="new-model-query"></a>新模型查询

使用新模型查询对话框创建新模型查询。 您可以将任何内容将在此处放置到一个常规`dx`命令。

例如，指定`Debugger.Sessions`检查调试器会话对象。 

![新数据模型查询对话框](images/windbgx-data-model-new-model-dialog.png)

有关调试器的一般信息的对象引用[dx （显示调试器对象模型表达式）](dx--display-visualizer-variables-.md)。

使用 LINQ 查询来深入到会话。 此查询显示正在运行的大多数线程前 5 个进程。 

```dbgcmd
Debugger.Sessions.First().Processes.Select(p => new { Name = p.Name, ThreadCount = p.Threads.Count() }).OrderByDescending(p => p.ThreadCount),5
```
![数据模型浏览窗口显示进程和线程](images/windbgx-data-model-process-threads.png)


## <a name="data-model-explorer"></a>数据模型资源管理器

使用数据模型资源管理器快速浏览在每个数据模型对象`Debugger`命名空间。

![数据模型资源管理器窗口中显示调试对象会话](images/windbgx-data-model-explore-window.png)


## <a name="change-query"></a>更改查询

使用更改查询以更改活动的数据模型窗口中使用的查询。


## <a name="display-mode"></a>显示模式

使用显示模式网格和层次结构显示模式之间切换。 您可以右键单击列标题以隐藏或显示更多的列。

网格模式可以是有用的对象中向下深入了解。 例如，下面是在网格视图中的上一个查询中 top 的线程。 

![数据模型浏览窗口中显示顶级线程](images/windbgx-data-model-process-threads-grid.png)

单击的任何带下划线的项目打开一个新选项卡和一个查询时运行可显示该信息。


此查询显示在插设备树中按物理设备对象的驱动程序的名称分组的设备。

```dbgcmd
Debugger.Sessions.First().Devices.DeviceTree.Flatten(n => n.Children).GroupBy(n => n.PhysicalDeviceObject->Driver->DriverName.ToDisplayString()) 
```
![数据模型浏览插设备树显示在网格视图窗口](images/windbgx-data-model-pnp-device.png)

---
 
## <a name="see-also"></a>请参阅

[dx （显示调试器对象模型表达式）](dx--display-visualizer-variables-.md)

[调试使用 WinDbg 预览](debugging-using-windbg-preview.md)
 

 





