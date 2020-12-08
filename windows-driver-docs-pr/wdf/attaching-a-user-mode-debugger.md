---
title: 附加用户模式调试程序
description: 附加用户模式调试程序
keywords:
- 附加用户模式调试器 WDK UMDF
- 多设备调试器附件 WDK UMDF
- 单设备调试器附件 WDK UMDF
- User-Mode Driver Framework WDK，用户模式调试器
- UMDF WDK，用户模式调试器
- 用户模式调试器 WDK UMDF
- 用户模式调试器 WDK UMDF，附加
- 用户模式驱动程序 WDK UMDF，调试
- 调试驱动程序 WDK UMDF，附加用户模式调试器
- 驱动程序调试 WDK UMDF，附加用户模式调试器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 166da51532976b4cbc3a43fef4dd9c2348aa1067
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96815789"
---
# <a name="attaching-a-user-mode-debugger"></a>附加用户模式调试程序


驱动程序管理器启动设备的驱动程序主机进程后，可以附加用户模式调试器。 如何附加调试器取决于连接到计算机的设备数：

-   如果已附加单个设备，请运行以下命令：

    ```cpp
    windbg -pn WUDFHost.exe
    ```

    重复运行此命令，直到发现调试的主机进程。

-   如果附加了多个设备，请确定特定主机的进程标识符 (PID) ，并运行以下命令：

    ```cpp
    windbg -p PID
    ```

    您可以使用操作系统提供的 Tasklist.exe 确定主机进程的 PID。  ( # A0 是一个命令行应用程序，该应用程序向用户提供在操作系统上运行的进程的列表。 ) 

 

 





