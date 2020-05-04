---
title: WinDbg 预览版-远程、进程服务器和转储文件会话
description: 本部分介绍如何使用 WinDbg 预览调试器启动远程进程服务器和转储文件会话。
ms.date: 01/10/2020
ms.localizationpriority: medium
ms.openlocfilehash: 1a204734b8a2dcaccfc9be1306ca3bcd763838e8
ms.sourcegitcommit: 44bccc9788690ae636b17d7d1cc576b8a17c9916
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81679218"
---
# <a name="windbg-preview---start-a-remote-process-server-and-dump-file-session"></a>WinDbg 预览版-启动远程进程服务器和转储文件会话

![windbg 预览版上的小徽标](images/windbgx-preview-logo.png)

本部分介绍如何使用 WinDbg 预览调试器启动远程进程服务器和转储文件会话。

## <a name="remote-debug-server"></a>远程调试服务器

使用此选项连接到远程调试服务器。

!["启动调试远程调试服务器" 对话框显示空白连接屏幕](images/windbgx-remote-session.png)

远程调试涉及两个在两个不同位置运行的调试器。 执行调试的调试器称为调试服务器。 第二个调试器（称为调试客户端）从远程位置控制调试会话。 若要建立远程会话，必须首先设置调试服务器，然后使用调试客户端连接到该服务器。

有关远程会话的详细信息，请参阅[使用 WinDbg 进行远程调试](remote-debugging-using-windbg.md)。

## <a name="process-debug-server"></a>处理调试服务器

通过进程服务器进行远程调试涉及运行服务器计算机上名为进程服务器的小型应用程序。 然后，在客户端计算机上启动用户模式调试器。 由于此调试器将执行所有实际处理，因此它被称为智能客户端。

有关进程服务器会话的详细信息，请参阅[进程服务器（用户模式）](process-servers--user-mode-.md)。

## <a name="open-a-dump-file"></a>打开转储文件

若要打开转储文件，请在提供的文件对话框中浏览到所需的文件并将其打开。

有关不同类型的转储文件的详细信息，请参阅[使用 WinDbg 分析故障转储文件](crash-dump-files.md)。

---

## <a name="see-also"></a>另请参阅

[使用 WinDbg 预览版进行调试](debugging-using-windbg-preview.md)
