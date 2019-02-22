---
title: Remote.exe 批处理文件
description: Remote.exe 批处理文件
ms.assetid: e774d39f-4625-41e7-9309-9dbdd46e986e
keywords:
- remote.exe，批处理文件通过远程调试
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: e046856486e044f6c0cf6fb2d229fbebf6ab51a9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526363"
---
# <a name="remoteexe-batch-files"></a>Remote.exe 批处理文件


## <span id="ddk_remote_exe_batch_files_dbg"></span><span id="DDK_REMOTE_EXE_BATCH_FILES_DBG"></span>


作为使用 remote.exe 进行远程调试的更多详细示例，假设三台计算机的内核调试方案中的本地主机计算机有关的以下信息：

-   调试需要进行接管 COM2 上的调制解调器电缆的位置。

-   符号文件是在文件夹 c:\\winnt\\符号。

-   在中创建一个名为 debug.log 的日志文件**c:\\temp**。

日志文件包含的所有内容在调试屏幕上看到在调试会话期间的副本。 从执行调试的人员的所有输入和目标系统上的内核调试器的所有输出写入该日志文件。

本地主机上运行调试会话的示例批处理文件是：

```bat
set _NT_DEBUG_PORT=com2
set _NT_DEBUG_BAUD_RATE=19200
set _NT_SYMBOL_PATH=c:\winnt\symbols
set _NT_LOG_FILE_OPEN=c:\temp\debug.log
remote /s "KD -v" debug
```

**请注意**  如果此批处理文件不在与 Remote.exe，相同的目录并且 Remote.exe 不在系统路径中列出的目录，则调用 Remote.exe 此批处理文件中的时，应在实用程序提供完整路径。

 

运行此批处理文件后，已被连接到本地主机计算机的 Windows 计算机的任何人都可以使用以下命令来连接到调试会话：

```console
remote /c computername debug 
```

其中*computername*是本地主机计算机的 NetBIOS 名称。

 

 





