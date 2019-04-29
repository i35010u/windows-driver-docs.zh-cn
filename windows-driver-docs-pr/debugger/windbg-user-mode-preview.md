---
title: WinDbg 预览-启动用户模式会话
description: 本部分介绍如何使用 WinDbg 预览调试器启动的用户模式会话。
ms.date: 08/04/2017
ms.localizationpriority: medium
ms.openlocfilehash: c27d3ada4127adb697eb81349c7212afa67597df
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390049"
---
# <a name="windbg-preview---start-a-user-mode-session"></a>WinDbg 预览-启动用户模式会话  

本部分介绍如何使用 WinDbg 预览调试器启动的用户模式会话。

选择*文件*，*开始调试*，并选择这四个选项之一：

- *启动可执行文件*-启动可执行文件并将其附加到它通过浏览的目标。
- *启动可执行文件 （高级）* -启动可执行文件并将附加到它使用一系列对话框使用高级选项。
- *附加到进程*-将附加到现有进程。
- *启动应用包*-启动并将附加到应用程序包。

此处介绍了所有四个选项。


## <a name="launch-executable"></a>启动可执行文件

使用此选项将启动的可执行文件并附加到它。

浏览到所需的可执行文件中提供的文件对话框，并将其打开。 


## <a name="launch-executable-advanced"></a>启动可执行文件 （高级）

使用此选项以启动可执行文件并将连接到该文本框中的一组使用高级选项。 

指定以下选项：
- 可执行文件，路径如*C:\Windows\notepad.exe*
- 可执行文件启动时提供的可选参数
- 可选的开始目录位置

![启动可执行文件 （高级） 使用高级选项的对话框](images/windbgx-launch-executable-advanced.png)


## <a name="attach-to-a-process"></a>附加到进程

使用此选项可附加到现有进程。

选择*显示所有用户的进程*以都显示其他进程。

> [!NOTE]
> 使用 UAC 盾项将需要进行提升以附加调试器。

在使用对话框下拉*附加*按钮以选择*非入侵性附加*。

![启动可执行文件 （高级） 使用高级选项的对话框](images/windbgx-attach-to-a-process.png)


## <a name="launch-app-package"></a>启动应用包

使用此选项以启动并附加到应用程序包。 使用搜索框查找特定的应用程序或后台任务。 使用包的详细信息按钮以显示有关包的信息。

![启动应用程序打包应用程序选项卡显示在搜索框中列出的三个应用 cal](images/windbgx-launch-app-package.png)


---

## <a name="see-also"></a>请参阅

[调试使用 WinDbg 预览](debugging-using-windbg-preview.md)






