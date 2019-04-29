---
title: U （Windows 调试器词汇表）
description: 术语表页-U
Robots: noindex, nofollow
ms.assetid: f3866ed9-eb94-4433-8a73-3b37f7e67303
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 41e8dd3ccb60e1af399873e003559c104440d7fc
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380771"
---
# <a name="u"></a>U


<span id="user_mode"></span><span id="USER_MODE"></span>**用户模式**  
在 Windows 中运行的应用程序和子系统*用户模式下*。 在用户模式下运行的进程执行此操作在其自己的虚拟地址空间内。 它们被限制直接访问系统，包括系统硬件，其使用，并可能危及系统完整性的系统的其他部分为未分配的内存的很多部分。 在用户模式下运行的进程是从系统和其他用户模式进程有效地隔离的因为它们不能干扰这些资源。

用户模式进程可分成以下类别：

-   系统进程

    这些执行重要功能，是操作系统的基本组成部分。 系统进程包括登录进程和会话管理器进程等项目。

-   服务器进程

    这些是事件日志和计划程序等的操作系统服务。 他们可以配置为在引导时自动启动。

-   环境子系统

    这些用于创建完整的操作系统环境的应用程序。 Windows 提供了以下三个环境：Win32、 POSIX 和 OS/2。

-   用户应用程序

    有五种类型：Win32、 Windows 3.1 中，Microsoft MS-DOS，POSIX 和 OS/2。

<span id="user_mode_debugging"></span><span id="USER_MODE_DEBUGGING"></span>**用户模式下调试**  
在用户模式下运行目标在其中一个调试器会话。

<span id="user_mode_target"></span><span id="USER_MODE_TARGET"></span>**用户模式目标**  
请参阅目标应用程序。

 

 





