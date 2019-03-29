---
title: 强制系统崩溃
description: 强制系统崩溃
ms.assetid: db93b032-2ca7-4197-87dd-4ae77c328f60
keywords:
- 在系统发生崩溃概述
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3fa70c7824b0327ecc0cbc01ca47a7bd4b55885a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564412"
---
# <a name="forcing-a-system-crash"></a>强制系统崩溃


## <span id="ddk_forcing_a_system_crash_dbg"></span><span id="DDK_FORCING_A_SYSTEM_CRASH_DBG"></span>


内核模式转储文件后[启用](enabling-a-kernel-mode-dump-file.md)，大多数系统崩溃应导致要写入的崩溃文件和要显示在蓝色屏幕。

但是，有些不实际启动内核故障情况下，系统会冻结的时候。 此类冻结的可能症状包括：

-   鼠标指针移动，但不能执行任何操作。

-   所有视频被都冻结，鼠标指针不会移动，但会继续分页。

-   没有任何响应根本到鼠标或键盘，并且使用的磁盘。

如果存在经验丰富的调试技术人员，他或她可以挂接内核调试程序并分析此问题。 有关查找这种情况发生时的一些提示，请参阅[调试停止系统](debugging-a-stalled-system.md)。

但是，如果存在任何技术人员，不则您可能希望创建一个内核模式转储文件，并将其发送到非现场技术人员。 此转储文件可以用于分析错误的原因。

有两种方法要故意导致系统崩溃：

[从调试器强制系统崩溃](forcing-a-system-crash-from-the-debugger.md)

[从键盘强制系统崩溃](forcing-a-system-crash-from-the-keyboard.md)

 

 





