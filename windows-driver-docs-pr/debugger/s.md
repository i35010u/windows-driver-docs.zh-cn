---
title: S （Windows 调试器词汇表）
description: 术语表页-S
Robots: noindex, nofollow
ms.assetid: 94cbf33b-e975-49eb-a266-774798955a48
keywords:
- 挂起的线程
- 挂起的进程
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2c583ab9cf7b5c6c1bbd8244d028ce2667b026ce
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366408"
---
# <a name="s"></a>S


<span id="scope"></span><span id="SCOPE"></span>**scope**  
定义本地变量的上下文。 该作用域具有三个组件： 一个堆栈帧、 当前指令和寄存器上下文。

有时称为*本地上下文*或*词法范围*。

<span id="second_chance_exception"></span><span id="SECOND_CHANCE_EXCEPTION"></span>**第二个可能发生的异常**  
第二个机会处理异常。 如果第一次机会在不处理异常，则仅提供这个机会。

<span id="smart_client"></span><span id="SMART_CLIENT"></span>**智能客户端**  
调试器引擎作为主机的实例。 智能客户端连接到进程服务器。 或 KD 连接服务器。

<span id="specific_exception_filter"></span><span id="SPECIFIC_EXCEPTION_FILTER"></span>**特定的异常筛选器**  
引擎对其具有内置筛选器异常事件筛选器。 最具体的异常筛选器是指特定类型的异常 （由异常代码标识），但默认异常筛选器也被称为特定异常筛选器。

<span id="specific_event_filter"></span><span id="SPECIFIC_EVENT_FILTER"></span>**特定事件筛选器**  
不是异常的事件的事件筛选器。 中列出的特定事件筛选器[**调试\_筛选器\_XXX**](https://docs.microsoft.com/windows-hardware/drivers/debugger/debug-filter-xxx)。

<span id="specific_filter"></span><span id="SPECIFIC_FILTER"></span>**特定筛选器**  
事件筛选器引擎对其具有内置筛选器的事件。

<span id="software_breakpoint"></span><span id="SOFTWARE_BREAKPOINT"></span>**software breakpoint**  
由调试器实现断点引擎临时修改目标的可执行代码。 执行代码时，触发断点。 修改代码是调试器或调试器引擎 API 的用户不可见。

<span id="stack"></span><span id="STACK"></span>**stack**  
查看调用堆栈。

<span id="stack_frame"></span><span id="STACK_FRAME"></span>**堆栈帧**  
包含单个函数调用的数据的调用堆栈中的内存。 这包括返回地址传递给函数和本地变量的参数。

<span id="stop_code"></span><span id="STOP_CODE"></span>**停止代码**  
请参阅错误检查代码。

<span id="stop_error"></span><span id="STOP_ERROR"></span>**停止错误**  
检查的 bug，请参阅。

<span id="stop_screen"></span><span id="STOP_SCREEN"></span>**停止屏幕**  
请参阅蓝屏。

<span id="subregister"></span><span id="SUBREGISTER"></span>**subregister**  
包含在另一个寄存器寄存器。 当 subregister 更改包含 subregister 的寄存器的部分也会更改。

<span id="suspended"></span><span id="SUSPENDED"></span>**suspended**  
如果它已被挂起目标、 进程或线程阻止执行。

<span id="symbol"></span><span id="SYMBOL"></span>**symbol**  
调试信息可提供有关目标在调试会话中的解释性信息的单元。 符号的示例包括变量 （本地和全局） 函数、 类型和函数的条目。 有关符号的信息可以包括名称、 类型 （如果适用），和地址或 regisgter 存储位置，以及任何父或子符号。 此信息存储在符号文件，并通常不是模块本身中提供。

符号文件不可用 （例如，导出符号），但这些符号通常提供仅极少信息时，调试器引擎可以合成某些符号。

<span id="symbol_file"></span><span id="SYMBOL_FILE"></span>**符号文件**  
创建生成的应用程序、 库、 驱动程序或操作系统时的补充文件。 符号文件包含的数据的实际时不需要运行这些二进制文件，但它会在调试过程中非常有用。

<span id="symbol_group"></span><span id="SYMBOL_GROUP"></span>**符号组**  
通常表示在作用域中的所有本地变量的符号的组。

<span id="symbol_type"></span><span id="SYMBOL_TYPE"></span>**符号类型**  
有关符号的表示形式，如在内存中其布局的描述性信息。 这是信息的编译器用于生成代码来操作该符号的一部分。 它还用于通过调试器引擎操作符号。 在符号文件中分发的符号类型。

<span id="synthetic_module"></span><span id="SYNTHETIC_MODULE"></span>**综合模块**  
该引擎将其视为一个模块的内存区域。 综合模块可能包含综合符号。

<span id="synthetic_symbol"></span><span id="SYNTHETIC_SYMBOL"></span>**综合符号**  
引擎将像一个符号内存地址。

<span id="system_crash"></span><span id="SYSTEM_CRASH"></span>**在系统发生崩溃**  
检查的 bug，请参阅。

 

 





