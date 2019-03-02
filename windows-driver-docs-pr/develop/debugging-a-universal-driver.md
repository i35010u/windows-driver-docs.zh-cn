---
title: 调试通用 Windows 驱动程序
description: 介绍可用于通用 Windows 驱动程序的调试技术。
ms.date: 06/09/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1cbe3724377ff559f52428bd983c76bcc6fcbcc1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56518490"
---
# <a name="debugging-a-universal-windows-driver"></a>调试通用 Windows 驱动程序

从 Windows 10 开始，可以生成 KMDF 或 UMDF 驱动程序二进制文件，这样它可以通过[即时跟踪记录器](https://msdn.microsoft.com/Library/Windows/Hardware/Dn914610)获取其他驱动程序调试信息。 通用 Windows 驱动程序可以利用此功能。

此外，如果你使用了 Visual Studio KMDF 模板，驱动程序将使用 Windows 软件跟踪预处理器 (WPP) 写入跟踪消息。 驱动程序二进制文件是具有提供程序 GUID 的 ETW 提供程序。

若要从驱动程序二进制文件发送跟踪消息，请使用以下代码：

   ```cpp
   TraceEvents(TRACE_LEVEL_INFORMATION, TRACE_DRIVER, &quot;%!FUNC! Entry&quot;);
   ```
       
可以通过手机上的 [TShell 工具](https://go.microsoft.com/fwlink/p/?linkid=617388)使用 Tracelog，或使用调试程序会话中的 [!wmitrace](https://msdn.microsoft.com/Library/Windows/Hardware/Ff561362) 访问 ETW 日志。

如何在手机上使用 Tracelog：

1.  在主计算机和手机之间建立内核模式调试会话。
2.  在主计算机上的 TShell 中输入此命令：

       ```cpp
       exec-device tracelog -addautologger MyLogger05 -guid c:\SteveGuid.txt -level 4 -flag 0xF –kd
       ```
       
3.  重新启动手机，观察调试程序中的跟踪消息。

所有现有的内核模式调试传输都会继续在 Windows 10 桌面版上运行。 但是，对于用户模式和内核模式驱动程序二进制文件，必须通过 KDNET 使用远程调试器会话来测试 Windows 10 移动版。 有关详细信息，请参阅“在 Visual Studio 中[通过网络电缆手动设置内核模式调试](https://msdn.microsoft.com/Library/Windows/Hardware/Hh439346)”。
