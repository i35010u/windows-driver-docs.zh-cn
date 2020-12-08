---
title: 手动调试服务应用程序
description: 手动调试服务应用程序
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 231e8ad2851d76ea7f29cf4f8a0b18aab97354a7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96819869"
---
# <a name="debugging-the-service-application-manually"></a>手动调试服务应用程序


在启动服务应用程序后手动附加到该服务应用程序非常类似于调试任何正在运行的用户模式进程。

使用带有 **/s** 选项的 [tlist.exe 工具](tlist.md)显示每个正在运行的进程的进程 ID (PID) 和每个进程中处于活动状态的服务。

如果要调试的服务应用程序与单个进程中的其他服务合并，则必须先将其隔离，然后再对其进行调试。 为此，请执行隔离服务中所述的过程。 在此过程结束时，请重新启动该服务。

若要确定服务的新 PID，请发出以下服务配置工具 ( # A0) 命令，其中 *ServiceName* 是服务的名称：

```console
sc queryex ServiceName 
```

现在，将此服务应用程序作为目标启动 WinDbg 或 CDB。 有三种方法可以实现此目的：通过使用-p 选项指定 PID，通过将指定名称与-pn 选项一起指定 (如果可执行文件的名称唯一) ，或通过使用-psn 选项指定服务名称。

例如，如果 SpoolSv.exe 的进程的 PID 为651，并且包含名为 *后台处理程序* 的服务，则以下三个命令是等效的：

```console
windbg -p 651 [AdditionalOptions] 
windbg -pn spoolsv.exe [AdditionalOptions] 
windbg -psn spooler [AdditionalOptions] 
```

调试器启动后，请像在任何其他用户模式调试会话中一样继续操作。

 

 





