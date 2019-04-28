---
title: 使用调试器和 Logexts.dll
description: 使用调试器和 Logexts.dll
ms.assetid: 7f7d3ca2-9b40-41ce-b66c-4367b93a7ff7
keywords:
- 记录器、 logexts.dll
- 记录器 CDB
- 记录器 WinDbg
- logexts.dll
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: e1538080047adc6ac27e8868268b2673e23e37c6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63340489"
---
# <a name="using-the-debugger-and-logextsdll"></a>使用调试器和 Logexts.dll


## <span id="ddk_using_the_debugger_and_logexts_dll_dtoolq"></span><span id="DDK_USING_THE_DEBUGGER_AND_LOGEXTS_DLL_DTOOLQ"></span>


若要激活记录器的一种方法是启动 CDB 或 WinDbg，像往常一样附加到用户模式下的目标应用程序。 然后，使用[ **！ logexts.logi** ](-logexts-logi.md)或[ **！ logexts.loge** ](-logexts-loge.md)扩展命令。

这将会关闭跳至的例程的加载和初始化 Logexts.dll 目标应用程序进程中的当前断点处插入代码。 这被称为"到目标应用程序注入记录器"。

将实际有两个实例的 Logexts.dll 运行，因为此模块是调试器扩展 DLL 和注入到目标应用程序的程序。 通过共享包含输出文件句柄、 当前类别掩码和指向日志输出缓冲区的指针的内存的一部分，Logexts.dll 的调试器和目标实例进行通信。

### <a name="span-idattachingtothetargetapplicationspanspan-idattachingtothetargetapplicationspanattaching-to-the-target-application"></a><span id="attaching_to_the_target_application"></span><span id="ATTACHING_TO_THE_TARGET_APPLICATION"></span>附加到目标应用程序

有关将调试器附加到目标应用程序的信息，请参阅[调试用户模式进程使用 WinDbg](debugging-a-user-mode-process-using-windbg.md)或[调试用户模式进程使用 CDB](debugging-a-user-mode-process-using-cdb.md)。

### <a name="span-idusingtheloggerextensioncommandsspanspan-idusingtheloggerextensioncommandsspanusing-the-logger-extension-commands"></a><span id="using_the_logger_extension_commands"></span><span id="USING_THE_LOGGER_EXTENSION_COMMANDS"></span>使用记录器扩展命令

每个扩展的完整语法，请参阅其引用页。

<span id="_LOGEXTS.LOGI"></span>[**!logexts.logi**](-logexts-logi.md)  
记录器注入目标应用程序。 此初始化日志记录，但不会启用它。

<span id="_LOGEXTS.LOGE"></span>[**!logexts.loge**](-logexts-loge.md)  
启用日志记录。 如果[ **！ logexts.logi** ](-logexts-logi.md)尚未使用，此扩展将初始化，并启用日志记录。

<span id="_LOGEXTS.LOGD"></span>[**!logexts.logd**](-logexts-logd.md)  
禁用日志记录。 这将导致所有 API 挂钩，为了允许自由地运行应用程序中删除。 COM 挂钩不会删除，因为它们不能随意重新启用。

<span id="_LOGEXTS.LOGO"></span>[**!logexts.logo**](-logexts-logo.md)  
显示或修改输出选项。 可使用三种类型的输出： 消息直接发送到调试器、 文本文件或.lgv 文件。 .Lgv 文件包含比其他两个; 的详细信息它可以与读取[日志查看器](logviewer.md)。

如果禁用文本文件输出，仍将创建大小为零的.txt 文件。 这可能会覆盖以前保存的文本文件，在同一位置。

<span id="_LOGEXTS.LOGC"></span>[**!logexts.logc**](-logexts-logc.md)  
显示可用 API 类别，将记录的类别并不是，这将的控件并显示包含的 Api 中的任何类别。

如果禁用某个类别，则将删除该类别中的所有 Api 的挂钩，以便不再对性能产生影响。 COM 挂钩不会删除，因为它们不能随意重新启用。

您只是想特定类型的程序具有与 Windows-例如，文件操作的交互时，允许仅特定类别可能会有用。 这可以减少日志文件大小，而且还可以减少的记录器进程的执行速度上产生的影响。

<span id="_LOGEXTS.LOGB"></span>[**!logexts.logb**](-logexts-logb.md)  
显示或刷新当前输出缓冲区。 作为性能的考虑因素，日志输出被刷新到磁盘仅当输出缓冲区已满时。 默认情况下，缓冲区为 2144 字节。

因为缓冲区内存由目标应用程序，如果发生访问冲突或某些其他不可恢复的错误目标应用程序中不会发生自动写入到磁盘上的日志文件的缓冲区。 在这种情况下，应使用此命令手动刷新到磁盘，缓冲区，否则最近日志记录 Api 可能不会显示在日志文件中。

<span id="_LOGEXTS.LOGM"></span>[**!logexts.logm**](-logexts-logm.md)  
显示或创建一个模块包含/排除列表。 通常是需要仅记录来自特定模块或一组的模块进行这些 API 调用。 若要使这更为简便，记录器，可指定模块包含列表，或者模块排除列表。 例如，如果您只希望记录中的一个或两个模块的调用将使用包含列表。 如果您想要日志从一个模块的简短列表除外的所有模块进行的调用，则会使用排除列表。 始终排除 Logexts.dll 和 Kernel32.dll 的模块，因为不允许使用记录器以记录本身。

 

 





