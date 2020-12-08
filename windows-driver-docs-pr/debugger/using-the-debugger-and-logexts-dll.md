---
title: 使用调试器和 Logexts.dll
description: 使用调试器和 Logexts.dll
keywords:
- 记录器，logexts.dll
- 记录器，CDB
- 记录器，WinDbg
- logexts.dll
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8b88f43c4506b06ddc0e582baabb3efd370f215e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803035"
---
# <a name="using-the-debugger-and-logextsdll"></a>使用调试器和 Logexts.dll


## <span id="ddk_using_the_debugger_and_logexts_dll_dtoolq"></span><span id="DDK_USING_THE_DEBUGGER_AND_LOGEXTS_DLL_DTOOLQ"></span>


激活记录器的一种方法是启动 CDB 或 WinDbg，并照常附加到用户模式目标应用程序。 然后，使用 [**！ logexts; logi**](-logexts-logi.md) 或 [**！ logexts。 loge**](-logexts-loge.md) extension 命令。

这将在当前断点处插入代码，该代码将跳转到在目标应用程序进程中加载和初始化 Logexts.dll 的例程。 这称为 "将记录器注入到目标应用程序中"。

实际上有两个 Logexts.dll 正在运行的实例，因为此模块既是调试器扩展 DLL，也是注入目标应用程序的程序。 Logexts.dll 的调试器和目标实例通过内存的共享部分进行通信，其中包括输出文件句柄、当前类别掩码和指向日志输出缓冲区的指针。

### <a name="span-idattaching_to_the_target_applicationspanspan-idattaching_to_the_target_applicationspanattaching-to-the-target-application"></a><span id="attaching_to_the_target_application"></span><span id="ATTACHING_TO_THE_TARGET_APPLICATION"></span>附加到目标应用程序

有关将调试器附加到目标应用程序的信息，请参阅 [使用 WinDbg 调试 User-Mode 进程](debugging-a-user-mode-process-using-windbg.md) 或 [使用 CDB 调试 User-Mode 进程](debugging-a-user-mode-process-using-cdb.md)。

### <a name="span-idusing_the_logger_extension_commandsspanspan-idusing_the_logger_extension_commandsspanusing-the-logger-extension-commands"></a><span id="using_the_logger_extension_commands"></span><span id="USING_THE_LOGGER_EXTENSION_COMMANDS"></span>使用记录器扩展命令

有关每个扩展的完整语法，请参阅其引用页。

<span id="_LOGEXTS.LOGI"></span>[**！ logexts. logi**](-logexts-logi.md)  
将记录器注入到目标应用程序中。 这会初始化日志记录，但不会启用日志记录。

<span id="_LOGEXTS.LOGE"></span>[**!logexts.loge**](-logexts-loge.md)  
启用日志记录。 如果未使用 [**！ logexts**](-logexts-logi.md) ，则此扩展将初始化，然后启用日志记录。

<span id="_LOGEXTS.LOGD"></span>[**!logexts.logd**](-logexts-logd.md)  
禁用日志记录。 这将导致删除所有 API 挂钩，以使程序可以自由运行。 不会删除 COM 挂钩，因为它们不能在需要时重新启用。

<span id="_LOGEXTS.LOGO"></span>[**！ logexts**](-logexts-logo.md)  
显示或修改输出选项。 可以使用三种类型的输出：直接发送到调试器、文本文件或 lgv 文件的消息。 Lgv 文件包含的信息远远多于其他两个，可以通过 [LogViewer](logviewer.md)读取。

如果禁用文本文件输出，则仍将创建大小为零的 .txt 文件。 这可能会覆盖同一位置中以前保存的文本文件。

<span id="_LOGEXTS.LOGC"></span>[**!logexts.logc**](-logexts-logc.md)  
显示可用的 API 类别，控制将记录哪些类别，哪些类别不会，并显示包含在任何类别中的 Api。

如果已禁用某一类别，则将删除该类别中所有 Api 的挂钩，以便不再出现任何性能开销。 不会删除 COM 挂钩，因为它们不能在需要时重新启用。

仅当对程序与 Windows 有关的特定类型的交互（例如，文件操作）感兴趣时，才启用特定类别会很有用。 这会减少日志文件的大小，还会减少记录器对进程执行速度产生的影响。

<span id="_LOGEXTS.LOGB"></span>[**！ logexts. logb**](-logexts-logb.md)  
显示或刷新当前输出缓冲区。 作为性能方面的考虑，仅当输出缓冲区已满时才将日志输出刷新到磁盘。 默认情况下，缓冲区为2144字节。

由于缓冲区内存由目标应用程序管理，因此，如果在目标应用程序中出现访问冲突或其他不可恢复的错误，则不会将缓冲区自动写入磁盘上的日志文件。 在这种情况下，应使用此命令手动将缓冲区刷新到磁盘，否则最近记录的 Api 可能不会出现在日志文件中。

<span id="_LOGEXTS.LOGM"></span>[**!logexts.logm**](-logexts-logm.md)  
显示或创建模块包含/排除列表。 通常，只需记录从某个模块或模块集发出的 API 调用。 为了便于使用，记录器可以指定模块包含列表或模块排除列表。 例如，如果只想记录一个或两个模块中的调用，则应使用包含列表。 如果你想要记录来自所有模块的调用，而不是较短的模块列表，则可以使用排除列表。 始终会排除 Logexts.dll 和 Kernel32.dll 模块，因为记录器不允许记录自身。

 

 





