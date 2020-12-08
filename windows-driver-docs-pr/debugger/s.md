---
title: 'S (Windows 调试器词汇表) '
description: 词汇表页-S
keywords:
- 挂起的线程
- 挂起的进程
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 40c0ebcac8694403da8dc37f3283c6cf4432db43
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96830247"
---
# <a name="s"></a>S


<span id="scope"></span><span id="SCOPE"></span>**内**  
定义局部变量的上下文。 作用域包含三个组件：堆栈帧、当前指令和寄存器上下文。

有时称为 " *本地上下文* " 或 " *词法范围*"。

<span id="second_chance_exception"></span><span id="SECOND_CHANCE_EXCEPTION"></span>**第二次异常**  
处理异常的第二个机会。 仅在第一次机会未处理异常的情况下才提供此机会。

<span id="smart_client"></span><span id="SMART_CLIENT"></span>**智能客户端**  
充当主机的调试器引擎的实例。 智能客户端连接到进程服务器。 或 KD 连接服务器。

<span id="specific_exception_filter"></span><span id="SPECIFIC_EXCEPTION_FILTER"></span>**特定异常筛选器**  
异常的事件筛选器，其中引擎具有内置筛选器。 大多数特定的异常筛选器都是指由异常代码)  (标识的特定类型的异常，但默认异常筛选器也限定为特定的异常筛选器。

<span id="specific_event_filter"></span><span id="SPECIFIC_EVENT_FILTER"></span>**特定事件筛选器**  
不是异常的事件的事件筛选器。 特定的事件筛选器在 [**调试 \_ 筛选器 \_ XXX**](./debug-filter-xxx.md)中列出。

<span id="specific_filter"></span><span id="SPECIFIC_FILTER"></span>**特定筛选器**  
事件的事件筛选器，其中引擎具有内置筛选器。

<span id="software_breakpoint"></span><span id="SOFTWARE_BREAKPOINT"></span>**软件断点**  
调试器引擎实现的断点临时修改目标的可执行代码。 执行代码时，将触发断点。 代码修改对于调试器或调试器引擎 API 的用户是不可见的。

<span id="stack"></span><span id="STACK"></span>**重叠**  
请参阅调用堆栈。

<span id="stack_frame"></span><span id="STACK_FRAME"></span>**堆栈帧**  
包含单个函数调用的数据的调用堆栈中的内存。 这包括返回地址、传递给函数的参数以及局部变量。

<span id="stop_code"></span><span id="STOP_CODE"></span>**停止代码**  
请参阅 bug 检查代码。

<span id="stop_error"></span><span id="STOP_ERROR"></span>**停止错误**  
请参阅 bug 检查。

<span id="stop_screen"></span><span id="STOP_SCREEN"></span>**停止屏幕**  
请参阅蓝屏。

<span id="subregister"></span><span id="SUBREGISTER"></span>**subregister**  
包含在另一个寄存器中的寄存器。 当 subregister 更改时，包含 subregister 的寄存器部分也会发生更改。

<span id="suspended"></span><span id="SUSPENDED"></span>**状态**  
如果已阻止其执行，则会挂起目标、进程或线程。

<span id="symbol"></span><span id="SYMBOL"></span>**代号**  
调试信息的单位，在调试会话中提供有关目标的解释性信息。 符号的示例包括 (本地和全局) 、函数、类型和函数项的变量。 有关符号的信息可以包括名称、在适用的) 中键入 (，以及存储该名称的地址或 regisgter，以及所有父或子符号。 此信息存储在符号文件中，并且通常不在模块本身中提供。

当符号文件不可用时，调试器引擎可以合成某些符号 (例如，) 导出符号，但这些符号通常仅提供最少的信息。

<span id="symbol_file"></span><span id="SYMBOL_FILE"></span>**符号文件**  
构建应用程序、库、驱动程序或操作系统时创建的补充文件。 符号文件所包含的数据在运行二进制文件时实际上并不需要，但在调试过程中非常有用。

<span id="symbol_group"></span><span id="SYMBOL_GROUP"></span>**符号组**  
一组符号，通常表示范围中的所有局部变量。

<span id="symbol_type"></span><span id="SYMBOL_TYPE"></span>**符号类型**  
有关符号表示形式的描述性信息，例如其在内存中的布局。 这是编译器用来生成代码以操作符号的信息的一部分。 调试器引擎也使用它来操作符号。 符号类型在符号文件中进行分布。

<span id="synthetic_module"></span><span id="SYNTHETIC_MODULE"></span>**合成模块**  
引擎作为模块处理的内存区域。 合成模块可以包含合成符号。

<span id="synthetic_symbol"></span><span id="SYNTHETIC_SYMBOL"></span>**合成符号**  
引擎将其视为符号的内存地址。

<span id="system_crash"></span><span id="SYSTEM_CRASH"></span>**系统崩溃**  
请参阅 bug 检查。

 

