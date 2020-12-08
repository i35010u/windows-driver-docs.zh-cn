---
title: 'T (Windows 调试器词汇表) '
description: 词汇表页-T
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 18180bcab90910fb8d2b95aa6f9b93bef05945da
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96813915"
---
# <a name="t"></a>T


<span id="target"></span><span id="TARGET"></span>**靶**  
目标应用程序、目标计算机或转储目标。

有时称为 *调试对象* 。

<span id="target_application"></span><span id="TARGET_APPLICATION"></span>**目标应用程序**  
在用户模式下调试的应用程序。

<span id="target_computer"></span><span id="TARGET_COMPUTER"></span>**目标计算机**  
正在内核模式下调试的计算机。

<span id="target_id"></span><span id="TARGET_ID"></span>**目标 ID**  
目标的唯一标识符。

<span id="target_process"></span><span id="TARGET_PROCESS"></span>**目标进程**  
在用户模式调试中，是指目标应用程序中的操作系统进程。

在内核模式调试中，表示内核的虚拟进程。

<span id="target_thread"></span><span id="TARGET_THREAD"></span>**目标线程**  
在用户模式调试中，是目标应用程序中的操作系统线程。

在内核模式调试中，表示处理器的虚拟线程。

<span id="thread_context"></span><span id="THREAD_CONTEXT"></span>**线程上下文**  
切换线程时 Windows 保留的状态。 这与寄存器上下文类似，只是在寄存器上下文中有一些额外的仅限内核的处理器状态，而不是线程上下文。 在内核模式调试过程中，此额外状态作为寄存器提供。

有关详细信息，请参阅作用域和符号组。

<span id="transport_layer"></span><span id="TRANSPORT_LAYER"></span>**传输层**  
这会控制远程调试期间主机和目标计算机之间的通信。

<span id="trap"></span><span id="TRAP"></span>**捕获**  
请参阅 bug 检查。

<span id="type"></span><span id="TYPE"></span>**类别**  
请参阅符号类型。

 

 





