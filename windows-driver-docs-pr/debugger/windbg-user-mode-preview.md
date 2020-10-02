---
title: WinDbg 预览版-启动用户模式会话
description: 本部分介绍如何使用 WinDbg 预览调试器启动用户模式会话。
ms.date: 01/09/2020
ms.localizationpriority: medium
ms.openlocfilehash: 6b026a2f4d7af2e2a3ad613784d4e01680596d64
ms.sourcegitcommit: b3e38d06762246c77cedd8e82d740ebea104c538
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2020
ms.locfileid: "91662471"
---
# <a name="windbg-preview---start-a-user-mode-session"></a>WinDbg 预览版-启动用户模式会话

![windbg 预览版上的小徽标](images/windbgx-preview-logo.png)

本部分介绍如何使用 WinDbg 预览调试器启动用户模式会话。

选择 " *文件*"、" *启动调试*"，然后选择以下四个选项之一：

- *启动可执行文件* -通过浏览目标来启动可执行文件并附加到它。
- *启动可执行文件 (advanced) * -启动可执行文件并使用一组具有高级选项的对话框附加到它。
- *附加到进程* -附加到现有进程。
- *启动应用程序包* -启动并附加到应用程序包。

此处描述了所有四个选项。

## <a name="launch-executable"></a>启动可执行文件

使用此选项可启动可执行文件并附加到它。

在提供的文件对话框中浏览到所需的可执行文件，然后将其打开。 

## <a name="launch-executable-advanced"></a>启动可执行文件 (高级) 

使用此选项可启动可执行文件并使用具有高级选项的一组文本框附加到该可执行文件。 

指定以下选项：
- 可执行文件的路径，例如 *C:\Windows\notepad.exe*
- 要在启动时提供给可执行文件的可选参数
- 可选的启动目录位置
- 目标位数、自动32或64。
- 启用调试子进程
- 带有时间行程调试的记录

![屏幕截图，显示 "启动可执行文件 (高级") "对话框，其中包含高级选项。](images/windbgx-launch-executable-advanced.png)

## <a name="attach-to-a-process"></a>附加到进程

使用此选项可附加到现有进程。

选择 " *显示所有用户的进程* " 以显示其他进程。

使用 "搜索" 框来筛选进程列表，例如通过搜索 SystemApps。

> [!NOTE]
> 带有 UAC 盾牌的项将需要提升调试器才能附加。

使用 " *附加* " 按钮上的下拉对话框选择 *非侵害性连接*。

![通过高级选项启动可执行文件 (高级) 对话框](images/windbgx-attach-to-a-process.png)

## <a name="launch-app-package"></a>启动应用程序包

使用此选项可以使用后台任务选项卡的应用程序启动并附加到应用程序包。 使用搜索框查找特定的应用程序或后台任务。 使用 "包详细信息" 按钮显示有关包的信息。

![“启动应用包”的“应用程序”选项卡，显示了搜索框中的“cal”，并列出了三个应用](images/windbgx-launch-app-package.png)

---

## <a name="see-also"></a>另请参阅

[使用 WinDbg 预览版进行调试](debugging-using-windbg-preview.md)
