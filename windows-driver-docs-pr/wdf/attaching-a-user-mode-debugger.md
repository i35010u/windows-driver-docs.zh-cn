---
title: 附加用户模式调试程序
description: 附加用户模式调试程序
ms.assetid: ba8eeabd-946d-46fa-b9ed-b9a674315bd4
keywords:
- 将用户模式下附加调试器 WDK UMDF
- 多个设备调试器附件 WDK UMDF
- 单个设备调试器附件 WDK UMDF
- 用户模式驱动程序框架 WDK，用户模式下调试程序
- UMDF WDK，用户模式下调试程序
- 用户模式下调试程序 WDK UMDF
- 用户模式下调试程序 WDK UMDF，附加
- 用户模式驱动程序 WDK UMDF，调试
- 调试驱动程序 WDK UMDF，将用户模式调试器附加
- 驱动程序调试 WDK UMDF，将用户模式调试器附加
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f712d2f24d038920b70f6a4c8439bef03bdc0e08
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63330871"
---
# <a name="attaching-a-user-mode-debugger"></a>附加用户模式调试程序


驱动程序管理器启动设备的驱动程序主机进程后，可以将附加用户模式下调试程序。 如何将调试器附加取决于多少台设备连接到计算机：

-   如果连接了单个设备，运行以下命令：

    ```cpp
    windbg -pn WUDFHost.exe
    ```

    反复运行此命令，直到发现要调试主机进程。

-   如果连接了多个设备，确定特定主机的进程标识符 (PID)，并运行以下命令：

    ```cpp
    windbg -p PID
    ```

    可以使用操作系统提供 Tasklist.exe 以确定主机进程的 PID。 （Tasklist.exe 是为用户提供了一系列操作系统运行的进程的命令行应用程序。）

 

 





