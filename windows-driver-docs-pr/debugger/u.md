---
title: U （Windows 调试器术语表）
description: 词汇表 page-U
ms.assetid: f3866ed9-eb94-4433-8a73-3b37f7e67303
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 27e7a99269f473197137f9c6dd8ce02c0c01c17b
ms.sourcegitcommit: 48c4b6d3a504583d2f588ed892a4a281d4b58301
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/06/2019
ms.locfileid: "70387063"
---
# <a name="u"></a>U


<span id="user_mode"></span><span id="USER_MODE"></span>**用户模式**  
应用程序和子系统在*用户模式下*在 Windows 中运行。 在用户模式下运行的进程在其自己的虚拟地址空间内执行此操作。 它们受到限制，无法直接访问系统的多个部分，包括系统硬件、未分配给其使用的内存，以及可能危及系统完整性的系统的其他部分。 由于在用户模式下运行的进程有效地与系统和其他用户模式进程隔离，因此它们不能干扰这些资源。

用户模式进程可以分组为以下类别：

-   系统进程

    它们执行重要功能，并且是操作系统的有机组成部分。 系统进程包括诸如登录进程和会话管理器进程这样的项。

-   服务器进程

    这些是操作系统服务，如事件日志和计划程序。 它们可以配置为在启动时自动启动。

-   环境子系统

    这些用于为应用程序创建完整的操作系统环境。 Windows 提供以下三种环境：Win32、POSIX 和 OS/2。

-   用户应用程序

    有五种类型：Win32、Windows 3.1、Microsoft MS-DOS、POSIX 和 OS/2。

<span id="user_mode_debugging"></span><span id="USER_MODE_DEBUGGING"></span>**用户模式调试**  
一个调试器会话，在该会话中，目标在用户模式下运行。

<span id="user_mode_target"></span><span id="USER_MODE_TARGET"></span>**用户模式目标**  
请参阅目标应用程序。

 

 





