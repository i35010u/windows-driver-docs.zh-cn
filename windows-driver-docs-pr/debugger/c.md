---
title: C （Windows 调试器词汇表）
description: 术语表页-C
Robots: noindex, nofollow
ms.assetid: 295b05a3-e27f-4761-a562-7e87e25bfd3b
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 67cafefd6e476c1274871599301a7769e495c07a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547726"
---
# <a name="c"></a>C


<span id="c___expression"></span><span id="C___EXPRESSION"></span>**C + + 表达式**  
可以通过 c + + 表达式计算器计算的表达式。

<span id="c_call_stack"></span><span id="C_CALL_STACK"></span>**C 调用堆栈**  
查看调用堆栈。

<span id="call_stack"></span><span id="CALL_STACK"></span>**调用堆栈**  
包含表示由线程进行的函数调用每个线程的堆栈帧的组。 每次函数调用进行新的堆栈帧时推送到堆栈的顶部。 该函数返回时，会在堆栈中弹出堆栈帧。

有时称为或仅简单地名为。

<span id="callback_object"></span><span id="CALLBACK_OBJECT"></span>**回调对象**  
请参阅事件回叫，回叫，输入和输出回调。

<span id="checked_build"></span><span id="CHECKED_BUILD"></span>**已检验的版本**  
存在两个不同版本的每个基于 NT 的操作系统：

-   （或） 的 Windows 操作系统的最终用户版本。 有关详细信息，请参阅免费生成。
-   （或） 的 Windows 可作为测试和调试中的操作系统和内核模式驱动程序开发方面的帮助。 已检验的版本包含额外错误检查、 参数验证和调试在免费版中不可用的信息。 它可以更轻松地跟踪在系统软件问题的原因。 已检查的系统或驱动程序可以帮助隔离和跟踪会导致不可预知的行为，导致内存泄漏，或导致不正确的设备配置的驱动程序问题。

虽然已检验的版本提供了额外的保护，但它会占用比免费版的更多内存和磁盘空间。 系统和驱动程序的性能是速度较慢，因为由于参数检查和诊断消息的输出执行额外的代码路径，并使用内核函数的一些备用实现。

Windows 已检验的版本不应混淆，其内置于一种检查生成环境的 Windows Driver Kit (WDK) 的驱动程序。

<span id="child_symbol"></span><span id="CHILD_SYMBOL"></span>**子符号**  
中的另一个符号包含一个符号。 例如，在结构中成员的符号是符号的该结构的子级。

<span id="client"></span><span id="CLIENT"></span>**client**  
请参阅客户端对象。

<span id="client_object"></span><span id="CLIENT_OBJECT"></span>**客户端对象**  
客户端对象用于与调试器引擎的交互。 它保留每个客户端状态，并提供调试器引擎 API 中顶级的接口的实现。

<span id="client_thread"></span><span id="CLIENT_THREAD"></span>**客户端线程**  
在其中创建客户端对象中的线程。 一般情况下，可能只能从该线程调用客户端的方法。 调试器引擎使用此线程以使对客户端中注册的回调对象的所有调用。

<span id="code_breakpoint"></span><span id="CODE_BREAKPOINT"></span>**code breakpoint**  
请参阅软件断点。

<span id="crash_dump_file"></span><span id="CRASH_DUMP_FILE"></span>**崩溃转储文件**  
一个包含某些内存区域和其他与应用程序或操作系统相关的数据的快照文件。 可以存储和随后用于在更高版本时调试应用程序或操作系统的崩溃转储文件。

时应用程序崩溃，并且可以由特殊 Windows 例程创建内核模式崩溃转储文件，Windows 本身出现故障时，Windows 可以创建用户模式崩溃转储文件。 有多种不同类型的故障转储文件。

<span id="current_process"></span><span id="CURRENT_PROCESS"></span>**当前进程**  
当前控制调试器引擎过程。 事件发生时，当前进程设置为事件处理。

<span id="current_target"></span><span id="CURRENT_TARGET"></span>**当前目标**  
调试器引擎当前控制目标。 事件发生时，当前的目标设置为事件目标。

<span id="current_thread"></span><span id="CURRENT_THREAD"></span>**当前线程**  
当前控制调试器引擎线程。 事件发生时，当前线程设置为事件线程。

 

 





