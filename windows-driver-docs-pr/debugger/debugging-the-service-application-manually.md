---
title: 手动调试服务应用程序
description: 手动调试服务应用程序
ms.assetid: 9be3976f-dd56-42f2-ac85-1c5a1f87a4ee
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0b6b7f99f96c5e4ed5067ccfb1555b2636dd5329
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63350561"
---
# <a name="debugging-the-service-application-manually"></a>手动调试服务应用程序


已启动后手动附加到服务应用程序非常类似于调试任何正在运行的用户模式进程。

使用[TList 工具](tlist.md)与 **/s**选项以显示进程 ID (PID) 的每个正在运行的进程和服务在每个进程处于活动状态。

如果你想要调试服务应用程序与单个进程中的其他服务结合使用，你必须在调试前隔离。 若要执行此操作，执行隔离服务中所述的过程。 在此过程结束时，重新启动服务。

若要确定服务的新的 PID，发出以下服务配置工具 (Sc.exe) 命令，其中*ServiceName*是服务名称：

```console
sc queryex ServiceName 
```

现在启动 WinDbg 或 CDB 与此服务应用程序为目标。 有三种方法来执行此操作： 通过使用-p 选项，指定 PID，通过指定了-pn 选项 （如果可执行文件的名称是唯一的），可执行文件的名称或通过使用-psn 选项指定服务名称。

例如，如果 651 PID 并包含名为的服务过程 SpoolSv.exe*后台处理程序*，以下三个命令是等效的：

```console
windbg -p 651 [AdditionalOptions] 
windbg -pn spoolsv.exe [AdditionalOptions] 
windbg -psn spooler [AdditionalOptions] 
```

调试器启动后，继续像任何其他用户模式下调试会话中。

 

 





