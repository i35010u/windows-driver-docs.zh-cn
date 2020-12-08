---
title: 'D (Windows 调试器词汇表) '
description: 词汇表页面-D
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: cc8adb40ac734c85ea4437628ecffd7dcdfe9604
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96787799"
---
# <a name="d"></a>D


<span id="data_breakpoint"></span><span id="DATA_BREAKPOINT"></span>**数据断点**  
请参阅处理器断点。

<span id="dbgeng_extension"></span><span id="DBGENG_EXTENSION"></span>**DbgEng 扩展**  
基于 dbgeng 头文件中的原型的调试器扩展。 这些扩展使用调试器引擎 API 与调试器引擎通信。

<span id="debug_build"></span><span id="DEBUG_BUILD"></span>**调试生成**  
请参阅检查的生成。

<span id="debuggee"></span><span id="DEBUGGEE"></span>**对象**  
请参阅目标。

<span id="debugger"></span><span id="DEBUGGER"></span>**程序**  
使用调试器引擎的全部功能的调试器引擎应用程序。 例如，WinDbg、CDB、NTSD 和 KD 都是调试器。

<span id="debugger_console"></span><span id="DEBUGGER_CONSOLE"></span>**调试器控制台**  
一个虚构实体，表示调试器引擎输入的源和输出的目标。 实际上，调试器引擎只使用输入和输出回调，并且没有用于实现它们的概念。

通常情况下，将从调试器接收输入命令窗口并将输出发送到同一个窗口。 但输入和输出回调可以为输出提供许多其他多个源，例如远程连接、脚本文件和日志文件。

<span id="debugger_engine"></span><span id="DEBUGGER_ENGINE"></span>**调试器引擎**  
用于操作调试目标的库。 其接口基于 dbgeng 文件中的原型。 调试器、扩展和调试器引擎应用程序使用此方法。

<span id="debugger_engine_api"></span><span id="DEBUGGER_ENGINE_API"></span>**调试器引擎 API**  
用于控制调试器引擎行为的强大接口。 它可以由调试器、DbgEng 扩展和调试器引擎应用程序使用。 可在 dbgeng 头文件中找到此接口的原型。

<span id="debugger_engine_application"></span><span id="DEBUGGER_ENGINE_APPLICATION"></span>**调试器引擎应用程序**  
一个独立的应用程序，它使用调试器引擎 API 来控制调试器引擎。

<span id="debugger_extension"></span><span id="DEBUGGER_EXTENSION"></span>**调试器扩展**  
可在调试器中运行的外部函数。 每个扩展都从称为调试器扩展 DLL 的模块中导出。 调试器引擎通过调用 DLL 中的代码来调用调试器扩展。 某些调试器扩展附带了 Windows 调试工具。 您可以编写自己的扩展来自动执行任意数量的调试器功能，或自定义调试器可以访问的信息的输出。

也称为或。

<span id="debugger_extension_dll"></span><span id="DEBUGGER_EXTENSION_DLL"></span>**调试器扩展 DLL**  
包含调试器扩展的 DLL。 调试器引擎加载 DLL 时，这些扩展可在调试器中使用。

<span id="debugger_extension_library"></span><span id="DEBUGGER_EXTENSION_LIBRARY"></span>**调试器扩展库**  
请参阅调试器扩展 DLL。

<span id="debugging_client"></span><span id="DEBUGGING_CLIENT"></span>**调试客户端**  
作为代理的调试器引擎实例，将调试器命令和 i/o 发送到调试服务器。

<span id="debugging_server"></span><span id="DEBUGGING_SERVER"></span>**调试服务器**  
充当主机的调试器引擎实例，侦听来自调试客户端的连接。

<span id="debugging_session"></span><span id="DEBUGGING_SESSION"></span>**调试会话**  
调试会话是运行软件调试程序（如 WinDbg、KD 或 CDB）以调试软件组件、系统服务、应用程序或操作系统的实际操作。 还可以针对内存转储文件运行调试会话以进行分析。

调试会话在获取时开始，并一直持续到所有目标都被丢弃。

<span id="default_exception_filter"></span><span id="DEFAULT_EXCEPTION_FILTER"></span>**默认异常筛选器**  
适用于与任何其他异常筛选器不匹配的异常事件的事件筛选器。 默认异常筛选器是特定的异常筛选器。

<span id="dormant_mode"></span><span id="DORMANT_MODE"></span>**休眠模式**  
调试器程序正在运行，但没有目标或活动会话的状态。

<span id="downstream_store"></span><span id="DOWNSTREAM_STORE"></span>**下游存储**  
符号服务器创建的符号的缓存。 通常，此缓存位于本地计算机上，而符号存储区位于远程位置。 如果具有符号服务器链，则下游存储可以位于从符号存储区下游的任何计算机上。

<span id="dump_file"></span><span id="DUMP_FILE"></span>**转储文件**  
请参阅故障转储文件。

<span id="dump_target"></span><span id="DUMP_TARGET"></span>**转储目标**  
正在调试的故障转储文件。

 

 





