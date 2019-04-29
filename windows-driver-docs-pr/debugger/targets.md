---
title: 目标
description: 目标
ms.assetid: 103d9b0a-2d51-404e-b8b9-513465427f7b
keywords:
- 调试器引擎目标
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 623b9eed23754f965a5b23a4c691a0b970463dd7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380491"
---
# <a name="targets"></a>目标


[调试器引擎](introduction.md#debugger-engine)支持调试不同类型的目标，[用户模式下](#live--user-mode-targets)并[内核模式](#live--kernel-mode-targets)的目标、 实时的目标和崩溃转储文件，以及本地和远程目标。 有不同的方法，用于连接到这些不同类型的目标的引擎。

### <a name="span-idcrashdumpfilesspanspan-idcrashdumpfilesspancrash-dump-files"></a><span id="crash_dump_files"></span><span id="CRASH_DUMP_FILES"></span>故障转储文件

使用打开用户模式和内核模式崩溃转储文件[ **OpenDumpFile**](https://msdn.microsoft.com/library/windows/hardware/ff552322)。 它还可以从目标创建转储文件引擎[ **WriteDumpFile2**](https://msdn.microsoft.com/library/windows/hardware/ff561382)。

### <a name="span-idlive--user-mode-targetsspanspan-idlive--user-mode-targetsspanlive-user-mode-targets"></a><span id="live--user-mode-targets"></span><span id="LIVE--USER-MODE-TARGETS"></span>Live 用户模式目标

调试器引擎可以同时创建并附加到用户模式进程。

创建一个过程是通过提供命令行中，可以选择的初始目录和环境中的，新进程。 引擎可以连接到新进程，或当它连接到另一个进程时挂起新过程。 例如时调试客户端和服务器组成的应用程序，就可以创建一个处于挂起状态的客户端并将附加到已在运行服务器上，允许服务器断点之前在客户端运行和服务器，从而促使设置操作。

时从进程中分离，引擎可以根据需要保留正常运行的进程、 终止进程，或放弃 （留出它挂起，直到另一个调试器附加到它或它已终止） 的过程。

该引擎可以查询有关的所有用户模式进程运行的计算机上，包括进程 ID 和用于启动进程的可执行映像的名称的信息。 可以使用此信息来帮助查找要调试的进程。

### <a name="span-idlive--kernel-mode-targetsspanspan-idlive--kernel-mode-targetsspanlive-kernel-mode-targets"></a><span id="live--kernel-mode-targets"></span><span id="LIVE--KERNEL-MODE-TARGETS"></span>Live、 内核模式目标

该方法[ **AttachKernel** ](https://msdn.microsoft.com/library/windows/hardware/ff538145)连接到 Windows 内核调试器引擎。

### <a name="span-idremote-targetsspanspan-idremote-targetsspanremote-targets"></a><span id="remote-targets"></span><span id="REMOTE-TARGETS"></span>远程目标

当使用调试器引擎进行远程调试时，有可能两个额外的步骤：

1.  连接到主机引擎。 如果主机引擎不是本地引擎实例，使用[ **DebugConnect** ](https://msdn.microsoft.com/library/windows/hardware/ff540465)创建连接到主机引擎客户端对象。

2.  连接到进程服务器或内核连接服务器的主机引擎。 如果主机引擎不能直接连接到目标，它必须连接到进程服务器或内核服务器连接。

现在客户端可以指示主机引擎获取通过进程服务器或内核连接服务器的目标。

### <a name="span-idacquiringtargetsspanspan-idacquiringtargetsspanacquiring-targets"></a><span id="acquiring_targets"></span><span id="ACQUIRING_TARGETS"></span>获取目标

时获取目标，直到目标会生成一个事件才完成目标的收购。 通常情况下，这意味着首先调用某种方法来将调试器附加到目标，然后调用[ **WaitForEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff561229)以便生成一个事件的目标。 此仍包含 true 目标为故障转储文件，因为这些始终存储事件通常导致要创建的转储文件的事件。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关将附加到目标的详细信息，请参阅[连接到目标](connecting-to-targets.md)。

 

 





