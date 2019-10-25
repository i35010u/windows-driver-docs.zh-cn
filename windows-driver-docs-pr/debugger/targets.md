---
title: 目标
description: 目标
ms.assetid: 103d9b0a-2d51-404e-b8b9-513465427f7b
keywords:
- 调试器引擎，目标
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 057ef3a2beb9a317141b58add9fb2e1f6a9248f7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838810"
---
# <a name="targets"></a>目标


[调试器引擎](introduction.md#debugger-engine)支持调试不同类型的目标、[用户模式](#live--user-mode-targets)和[内核模式](#live--kernel-mode-targets)目标、实时目标和故障转储文件以及本地和远程目标。 可以通过不同的方法将引擎连接到这些不同类型的目标。

### <a name="span-idcrash_dump_filesspanspan-idcrash_dump_filesspancrash-dump-files"></a><span id="crash_dump_files"></span><span id="CRASH_DUMP_FILES"></span>故障转储文件

用户模式和内核模式故障转储文件都是通过[**OpenDumpFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-opendumpfile)打开的。 引擎还可以使用[**WriteDumpFile2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-writedumpfile2)从目标创建转储文件。

### <a name="span-idlive--user-mode-targetsspanspan-idlive--user-mode-targetsspanlive-user-mode-targets"></a><span id="live--user-mode-targets"></span><span id="LIVE--USER-MODE-TARGETS"></span>实时，用户模式目标

调试器引擎可以创建并附加到用户模式进程。

通过为新进程提供命令行和初始目录和环境，创建进程。 然后，引擎可以连接到新进程，或在连接到其他进程时保持新进程挂起。 例如，在调试同时包含客户端和服务器的应用程序时，可以创建处于挂起状态的客户端并将其附加到已在运行的服务器，以便在客户端运行和引发服务器之前设置服务器断点运算符.

从进程分离时，引擎可以根据需要保持进程正常运行，终止进程，或者放弃进程（使其暂停，直到另一个调试器附加到它或终止）。

此引擎可以查询有关计算机上运行的所有用户模式进程的信息，包括用于启动进程的可执行映像的进程 ID 和名称。 此信息可用于帮助查找要调试的进程。

### <a name="span-idlive--kernel-mode-targetsspanspan-idlive--kernel-mode-targetsspanlive-kernel-mode-targets"></a><span id="live--kernel-mode-targets"></span><span id="LIVE--KERNEL-MODE-TARGETS"></span>实时、内核模式目标

方法[**AttachKernel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-attachkernel)将调试器引擎连接到 Windows 内核。

### <a name="span-idremote-targetsspanspan-idremote-targetsspanremote-targets"></a><span id="remote-targets"></span><span id="REMOTE-TARGETS"></span>远程目标

使用调试器引擎进行远程调试时，可能需要执行两个额外的步骤：

1.  连接到主机引擎。 如果主机引擎不是本地引擎实例，请使用[**DebugConnect**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-debugconnect)创建连接到主机引擎的客户端对象。

2.  将主机引擎连接到进程服务器或内核连接服务器。 如果主机引擎未直接连接到目标，则它必须连接到执行的进程服务器或内核连接服务器。

现在，客户端可以告诉主机引擎通过进程服务器或内核连接服务器获取目标。

### <a name="span-idacquiring_targetsspanspan-idacquiring_targetsspanacquiring-targets"></a><span id="acquiring_targets"></span><span id="ACQUIRING_TARGETS"></span>获取目标

获取目标时，在目标生成事件之前，不会完成目标的获取。 通常，这意味着首先调用方法将调试器附加到目标，然后调用[**WaitForEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-waitforevent)来使目标生成事件。 当目标是故障转储文件时，这仍然为 true，因为它们始终存储事件-通常是导致创建转储文件的事件。

### <a name="span-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关附加到目标的详细信息，请参阅[连接到目标](connecting-to-targets.md)。

 

 





