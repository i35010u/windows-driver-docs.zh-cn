---
title: 设置测试系统
description: 设置测试系统
keywords:
- 测试网络组件升级 WDK
- 升级测试 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 03c469c9821fc5177eacf96f2b82705c9165e553
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96819995"
---
# <a name="setting-up-the-test-system"></a>设置测试系统





**注意**  Microsoft Windows XP (SP1 及更高版本) 、Microsoft Windows Server 2003 和更高版本的操作系统不支持供应商提供的网络升级。

 

升级网络组件之前，请确保正确安装和配置要升级的网络组件。

**设置测试系统**

1.  为 preupgrade 操作系统创建一个分区，为 Microsoft Windows 2000 或更高版本的操作系统创建另一个分区。
    **注意**  请勿在同一分区中安装 preupgrade 操作系统和升级操作系统。 如果在同一分区中安装了 preupgrade 操作系统和 Windows 2000 或更高版本，则它们将共享同一程序文件目录。

     

2.  在测试系统上，启动不是要升级的操作系统版本。 然后，将整个分区（pagefile.sys 文件除外）复制到备份目录中。 不需要复制 pagefile.sys 文件，因为它是在 Windows 2000 或更高版本的启动时创建的。

    这种创建备份安装的方法优于创建磁盘映像程序，因为它允许你使用 **xcopy**，这会花费比磁盘映像程序更少的时间来复制文件。 只需将备份分区的内容复制到要升级的新分区即可重复升级测试;无需重新安装 preupgrade 操作系统。

3.  创建一个用于存储网络迁移 DLL 和 netmap 文件的测试目录，然后将这些文件复制到测试目录。

4.  创建另一个目录，用于存储 Winnt32.exe 升级阶段所需的 Windows 2000 或更高版本的文件。

5.  将 Windows 2000 或更高版本的驱动程序开发工具包 (DDK) 包含 Windows 2000 或更高版本的已检查内部版本的 cd-rom 上。 从 cd-rom \\ 上的 i386 目录中，将以下文件复制到备份目录， (步骤 2) ：
    -   winnt32.exe
    -   winnt32u.dll
    -   pidgen.dll
    -   wetuplog.\*

6.  创建名为 winntupg 的升级目录。 将 cd-rom 上的 i386 winntupg 目录中的文件复制 \\ \\ 到测试系统上的 winntupg 目录。

7.  在文本系统上启用调试器，或在 Windows 2000 或更高版本操作系统的资源工具包中提供 debugmon.exe。 然后，将 netcfg.ini 文件复制到% windir%。 netcfg.ini 文件启用调试跟踪。

    下面是一个示例 netcfg.ini 文件：

    ```INI
    [DebugFlags]
    BreakOnAddLegacy=0
    BreakOnAlloc=0
    BreakonDoUnattend=0
    BreakonDwrefProblem=0
    BreakOnError=0
    BreakOnHr=0
    BreakOnHrInteraction=0
    BreakOnIteration=0
    BreakOnNetInstall=0
    BreakOnWizard=0
    DisableTray=0
    DumpLeaks=0
    DumpNetCfgTree=0
    NetShellBreakOnInit=0
    ShowIngnoreErrors=0
    ShowProcessAndThreadIds=0
    SkipLanEnum=0
    TracingTimeStamps=0

    [Default]
    OutputToDebug=1

    [EsLocks]
    OutputToDebug=0

    [ShellViewMsgs]
    OutputToDebug=0

    [OptErrors]
    OutputToDebug=0
    ```

 

 





