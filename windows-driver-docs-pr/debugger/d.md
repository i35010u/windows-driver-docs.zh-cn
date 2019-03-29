---
title: D （Windows 调试器词汇表）
description: 术语表页-D
Robots: noindex, nofollow
ms.assetid: e4d53375-c82e-493b-9ccb-444c211fbc79
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: a5b5f500adcae7bb675393b346f5d1b777943497
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56576796"
---
# <a name="d"></a>D


<span id="data_breakpoint"></span><span id="DATA_BREAKPOINT"></span>**data breakpoint**  
请参阅处理器断点。

<span id="dbgeng_extension"></span><span id="DBGENG_EXTENSION"></span>**DbgEng 扩展。**  
调试器扩展基于 dbgeng.h 标头文件中的原型。 这些扩展使用调试器引擎 API 与调试器引擎进行通信。

<span id="debug_build"></span><span id="DEBUG_BUILD"></span>**调试版本**  
请参阅调试内部版本。

<span id="debuggee"></span><span id="DEBUGGEE"></span>**debuggee**  
请参阅目标。

<span id="debugger"></span><span id="DEBUGGER"></span>**debugger**  
使用调试器引擎的完整功能的调试器引擎应用程序。 例如，WinDbg、 CDB、 NTSD 和 KD 是调试器。

<span id="debugger_console"></span><span id="DEBUGGER_CONSOLE"></span>**调试器控制台**  
一个虚构实体表示调试器引擎输入的源和目标的输出。 实际上，调试器引擎仅使用输入和输出回调并且不了解的内容用于实现它们。

通常情况下，在调试器命令窗口中收到输入和输出发送到同一个窗口。 但是，输入和输出回调可以提供许多其他源的输入和输出，例如，远程连接、 脚本文件和日志文件的目标。

<span id="debugger_engine"></span><span id="DEBUGGER_ENGINE"></span>**调试器引擎**  
用于处理调试目标库。 其界面基于 dbgeng.h 文件中的原型。 使用它通过调试器，扩展和调试器引擎应用程序。

<span id="debugger_engine_api"></span><span id="DEBUGGER_ENGINE_API"></span>**调试器引擎 API**  
若要控制调试器引擎的行为了强大接口。 可以使用它通过调试器，DbgEng 扩展和调试器引擎应用程序。 此接口的原型 dbgeng.h 标头文件中找到。

<span id="debugger_engine_application"></span><span id="DEBUGGER_ENGINE_APPLICATION"></span>**调试器引擎应用程序**  
使用调试器引擎 API 来控制调试器引擎的独立应用程序。

<span id="debugger_extension"></span><span id="DEBUGGER_EXTENSION"></span>**调试程序扩展**  
可以在调试器中运行一个外部函数。 每个扩展是从称为调试器扩展 DLL 的模块导出的。 调试器引擎通过调用其 DLL 中的代码调用调试器扩展。 某些调试器扩展预装的 Windows 调试工具。 您可以编写自己的扩展自动执行任意数量的调试器功能或自定义输出到调试器可访问的信息。

也称为，或只需。

<span id="debugger_extension_dll"></span><span id="DEBUGGER_EXTENSION_DLL"></span>**调试器扩展 DLL**  
包含调试器扩展的 DLL。 当调试器引擎加载 DLL 时变为可供这些扩展将使用在调试器中。

<span id="debugger_extension_library"></span><span id="DEBUGGER_EXTENSION_LIBRARY"></span>**调试器扩展插件库**  
请参阅调试器扩展 DLL。

<span id="debugging_client"></span><span id="DEBUGGING_CLIENT"></span>**调试客户端**  
调试器引擎充当代理，将调试器命令和 I/O 发送到调试服务器的实例。

<span id="debugging_server"></span><span id="DEBUGGING_SERVER"></span>**调试服务器**  
作为主机，侦听来自调试客户端连接的调试器引擎的实例。

<span id="debugging_session"></span><span id="DEBUGGING_SESSION"></span>**在调试会话**  
调试会话是运行调试程序，如 WinDbg、 KD 或 CDB，若要调试软件组件、 系统服务、 应用程序或操作系统软件的实际操作。 此外可以针对用于分析的内存转储文件运行调试会话。

启动调试会话时获取仅持续到所有目标已都放弃。

<span id="default_exception_filter"></span><span id="DEFAULT_EXCEPTION_FILTER"></span>**默认异常筛选器**  
适用于与任何其他异常筛选器不匹配的异常事件的事件筛选器。 默认异常筛选器是一个特定的异常筛选器。

<span id="dormant_mode"></span><span id="DORMANT_MODE"></span>**休眠模式**  
调试程序运行，但不带目标或活动的会话状态。

<span id="downstream_store"></span><span id="DOWNSTREAM_STORE"></span>**下游应用商店**  
创建符号服务器的符号的缓存。 通常此缓存是在本地计算机上而符号存储区位于远程。 如果你具有的符号服务器链，下游应用商店可以位于下游符号存储区中任何计算机上。

<span id="dump_file"></span><span id="DUMP_FILE"></span>**转储文件**  
请参阅崩溃转储文件。

<span id="dump_target"></span><span id="DUMP_TARGET"></span>**转储目标**  
正在调试崩溃转储文件。

 

 





