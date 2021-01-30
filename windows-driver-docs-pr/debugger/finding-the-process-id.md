---
title: 查找进程 ID
description: 查找进程 ID
keywords:
- '进程 ID (PID) '
- 'PID (进程 ID) '
- Tlist.exe，相关技术
- 任务管理器
ms.date: 01/29/2021
ms.localizationpriority: medium
ms.custom: contperf-fy21q3
ms.openlocfilehash: 12b695b7fcb0e0765a41ed8490f3e176fb7b6f93
ms.sourcegitcommit: 597ef5dc63565202a8c6d9e51c9faf1b6398968a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/29/2021
ms.locfileid: "99081121"
---
# <a name="finding-the-process-id"></a>查找进程 ID

将为 Windows 中运行的每个进程分配一个唯一的十进制数，称为进程 ID (PID) 。 使用此数字的方法有很多，例如，在将调试器附加到该进程时指定进程。

本主题介绍如何使用任务管理器、tasklist Windows 命令、Tlist.exe 实用工具或调试器来确定给定应用程序的 PID。

## <a name="task-manager"></a>任务管理器

可以通过多种方法打开任务管理器，但最简单的方法是选择 Ctrl + Alt + Delete，然后选择 " **任务管理器**"。

在 Windows 10 中，首先单击 " **更多详细信息** " 以展开显示的信息。  从 " **进程** " 选项卡中，选择 " **详细信息** " 选项卡以查看 *PID* 列中列出的进程 ID。

![Windows 10 中任务管理器的部分屏幕截图，显示进程编号，按用户名排序。](images/process-id-task-manager-windows-10.png)

单击任意要排序的列名称。 您可以右键单击进程名称以查看进程的更多选项。

某些内核错误可能会导致任务管理器的图形界面发生延迟。

## <a name="the-tasklist-command"></a>**Tasklist** 命令

使用命令提示符下的内置 Windows **tasklist** 命令显示所有进程、其 pid 以及各种其他详细信息。

```console
C:\>tasklist

Image Name                     PID Session Name        Session#    Mem Usage
========================= ======== ================ =========== ============
System Idle Process              0 Services                   0          8 K
System                           4 Services                   0      7,428 K
Secure System                  104 Services                   0     40,344 K
Registry                       164 Services                   0    146,596 K
smss.exe                       592 Services                   0      1,176 K
csrss.exe                      896 Services                   0      6,224 K
wininit.exe                    980 Services                   0      6,572 K
...
```

用于 `tasklist /?` 显示命令行帮助。

## <a name="tlist-utility"></a>Tlist.exe 实用程序

任务列表查看器 (Tlist.exe) 或 tlist.exe 是一个命令行实用工具，用于显示当前在本地计算机上运行的任务列表或用户模式进程。 Tlist.exe 包含在适用于 Windows 的调试工具中。 有关如何下载和安装调试工具的信息，请参阅 [下载适用于 Windows 的调试工具](debugger-download-tools.md)。

如果在64位计算机上的默认目录中安装了 Windows 驱动程序工具包，则调试工具位于此处：

`C:\Program Files (x86)\Windows Kits\10\Debuggers\x64\`

当你从命令提示符运行 Tlist.exe 时，它将在内存中显示具有唯一 PID 号的所有用户模式进程的列表。 对于每个进程，它将显示 PID、进程名称和，如果进程具有窗口，则显示该窗口的标题。

```console
C:\Program Files (x86)\Windows Kits\10\Debuggers\x64>tlist -t
System Process (0)
System (4)
  smss.exe (592)
  Memory Compression (3376)
Secure System (104)
Registry (164)
csrss.exe (896)
wininit.exe (980)
  services.exe (660)
    svchost.exe (1232)
      WmiPrvSE.exe (6008)
      dllhost.exe (1748)
      WmiPrvSE.exe (1860)
...
```

有关详细信息，请参阅 [tlist.exe](tlist.md)。

## <a name="the-tlist-debugger-command"></a>**Tlist.exe** 调试器命令

如果在相关系统上已经有一个用户模式调试器在运行，则 [**tlist.exe (列出进程 id)**](-tlist--list-process-ids-.md) 命令将显示该系统上所有 pid 的列表。

## <a name="powershell-get-process-command"></a>PowerShell Get-Process 命令

若要使用自动化脚本，请使用 Get-Process PowerShell 命令。 指定特定的进程名称，以查看该进程的进程 ID。

```powershell
C:\> Get-Process explorer

Handles  NPM(K)    PM(K)      WS(K)     CPU(s)     Id  SI ProcessName
-------  ------    -----      -----     ------     --  -- -----------
   2520     404   108948     179284   1,702.95   7656   1 explorer
```

有关详细信息，请参阅 [获取进程](/powershell/module/microsoft.powershell.management/get-process)。

## <a name="csrss-and-user-mode-drivers"></a>CSRSS 和用户模式驱动程序

若要调试在另一台计算机上运行的用户模式驱动程序，请 Run-Time 子系统 (CSRSS) 进程中调试客户端服务器。 有关详细信息，请参阅 [调试 CSRSS](debugging-csrss.md)。
