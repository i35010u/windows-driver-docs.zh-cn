---
title: Remote.exe 批处理文件
description: Remote.exe 批处理文件
keywords:
- 通过 remote.exe、批处理文件进行远程调试
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: cfb08da4fe0f59192f353a2075af6f57b165d342
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96831929"
---
# <a name="remoteexe-batch-files"></a>Remote.exe 批处理文件


## <span id="ddk_remote_exe_batch_files_dbg"></span><span id="DDK_REMOTE_EXE_BATCH_FILES_DBG"></span>


若要详细了解如何使用 remote.exe 进行远程调试，请在三台计算机内核调试方案中假设存在以下关于本地主机的信息：

-   需要在 COM2 上通过空调缆线进行调试。

-   符号文件位于文件夹 c： \\ winnt \\ 符号内。

-   在 **c： \\ temp** 中创建名为 "debug" 的日志文件。

日志文件保存在调试会话期间在调试屏幕上看到的所有内容的副本。 执行调试的人员的所有输入以及目标系统上的内核调试器的所有输出都将写入该日志文件。

在本地主机上运行调试会话的示例批处理文件是：

```bat
set _NT_DEBUG_PORT=com2
set _NT_DEBUG_BAUD_RATE=19200
set _NT_SYMBOL_PATH=c:\winnt\symbols
set _NT_LOG_FILE_OPEN=c:\temp\debug.log
remote /s "KD -v" debug
```

**注意**   如果此批处理文件与 Remote.exe 不在同一目录中，并且 Remote.exe 不在系统路径中列出的目录中，则应在调用此批处理文件中的 Remote.exe 时，为实用程序指定完整路径。

 

运行此批处理文件后，任何具有本地主机计算机网络的 Windows 计算机的用户都可以使用以下命令连接到调试会话：

```console
remote /c computername debug 
```

其中 *computername* 为本地主机计算机的 NetBIOS 名称。

 

 





