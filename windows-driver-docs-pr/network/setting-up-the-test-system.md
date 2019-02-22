---
title: 设置测试系统
description: 设置测试系统
ms.assetid: 99c591e0-fe01-4db9-af95-4ce458625bfb
keywords:
- 测试网络组件升级 WDK
- 升级测试 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 50d3a9cfe5b1ebf73d821da1197b53b286bca5db
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524625"
---
# <a name="setting-up-the-test-system"></a>设置测试系统





**请注意**  供应商提供网络升级不支持在 Microsoft Windows XP (SP1 和更高版本)，Microsoft Windows Server 2003 和更高版本操作系统。

 

升级网络组件之前，请确保要升级的网络组件正确安装和配置。

**若要设置的测试系统**

1.  创建一个分区的升级前的操作系统和 Microsoft Windows 2000 或更高版本操作系统的另一个分区。
    **请注意**  同一个分区中不能安装升级前的操作系统和升级操作系统。 如果升级前的操作系统和 Windows 2000 或更高版本安装在同一分区中，它们将共享相同的 Program Files 目录。

     

2.  在测试系统上，启动不是要升级的操作系统生成。 然后将复制整个分区要升级，除了 pagefile.sys 文件到备份目录。 没有必要复制 pagefile.sys 文件，因为在启动时的 Windows 2000 或更高版本创建。

    创建备份安装的此方法时最好创建磁盘映像程序，因为它允许你使用**xcopy**，这将缩短时间将比磁盘映像程序文件复制。 您可以通过只需将备份分区的内容复制到新的分区要升级; 重复升级测试不需要重新安装升级前的操作系统。

3.  创建用于存储网络迁移 DLL 和 netmap.inf 文件中，一个测试目录，然后将这些文件复制到测试目录。

4.  创建用于存储在 Windows 2000 或更高版本为 Winnt32 升级阶段所需的文件的另一个目录。

5.  Windows 2000 或更高版本的驱动程序开发工具包 (DDK) 包含已检验的版本的 Windows 2000 或更高版本的 CD-ROM 插入。 从\\i386 目录在 CD-ROM 上的将以下文件复制到备份目录 (步骤 2):
    -   winnt32.exe
    -   winnt32u.dll
    -   pidgen.dll
    -   wetuplog。\*

6.  创建名为 winntupg 升级目录。 复制中的文件\\i386\\winntupg 到测试系统上的 winntupg 目录 CD-ROM 上的目录。

7.  启用文本系统上的调试器或启动 debugmon.exe，这是 Windows 2000 资源工具包或更高版本操作系统附带。 然后将 netcfg.ini 文件复制到 %windir%。 Netcfg.ini 文件启用调试跟踪。

    下面是示例 netcfg.ini 文件：

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

 

 





