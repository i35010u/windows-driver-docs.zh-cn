---
title: DbgSrv 命令行选项
description: DbgSrv 命令行使用以下语法。
keywords:
- DbgSrv Command-Line 选项 Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- DbgSrv Command-Line Options
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: bb04a08f0233a4ea6efe508a1ace108240f12294
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837827"
---
# <a name="dbgsrv-command-line-options"></a>DbgSrv 命令行选项


DbgSrv 命令行使用以下语法。

```console
dbgsrv -t ServerTransport [-sifeo image.ext] -c[s] AppCmdLine [-x | -pc] 

dbgsrv -? 
```

所有选项都区分大小写。

## <a name="span-idddk_dbgsrv_command_line_options_dbgspanspan-idddk_dbgsrv_command_line_options_dbgspanparameters"></a><span id="ddk_dbgsrv_command_line_options_dbg"></span><span id="DDK_DBGSRV_COMMAND_LINE_OPTIONS_DBG"></span>参数


<span id="_______-t_______ServerTransport______"></span><span id="_______-t_______servertransport______"></span><span id="_______-T_______SERVERTRANSPORT______"></span>**-t** *ServerTransport*   
指定传输协议。 有关每种情况下的可能协议列表和 *ServerTransport* 的语法，请参阅 [**激活进程服务器**](activating-a-process-server.md)。

<span id="_______-sifeo_______Executable______"></span><span id="_______-sifeo_______executable______"></span><span id="_______-SIFEO_______EXECUTABLE______"></span>**-sifeo** *可执行文件*   
挂起 (给定图像的 IFEO) 值的图像文件执行选项。 *可执行* 文件应包括可执行映像的文件名，包括文件扩展名。 -Sifeo 选项允许将 DbgSrv 设置为由-c 选项创建的映像的 IFEO 调试器，而不会由于 IFEO 设置而导致递归调用。 仅当使用-c 时，才能使用此选项。

<span id="_______-c______"></span><span id="_______-C______"></span>**-c**   
使 DbgSrv 创建新的进程。 可以使用它来创建要调试的进程。 这类似于从调试器生成新进程，但在创建此进程时 *不* 会对其进行调试。 若要调试此进程，请在启动智能客户端时确定其 PID 并使用 **-p** 选项来调试此进程。

<span id="_______s______"></span><span id="_______S______"></span>**s**   
导致立即挂起新创建的进程。 如果使用此选项，建议使用 CDB 作为智能客户端，并使用-pb 命令行选项启动智能客户端，并与-p PID 一起使用。 如果在命令行上包含-pb 选项，则当调试器附加到该进程时，该进程将继续进行;否则，可以通过 [**~ \* m**](-m--resume-thread-.md)命令继续执行此过程。

<span id="_______AppCmdLine______"></span><span id="_______appcmdline______"></span><span id="_______APPCMDLINE______"></span>*AppCmdLine*   
指定要创建的进程的完整命令行。 *AppCmdLine* 可以是 UNICODE 或 ASCII 字符串，可以包含任何可打印的字符。 出现在 **-c** s 参数之后的所有文本 \[ **s** \] 都将被视为字符串 *AppCmdLine*。

<span id="_______-x______"></span><span id="_______-X______"></span>**-x**   
导致忽略命令行的其余部分。 如果要从可向其命令行追加不需要的文本的应用程序启动 DbgSrv，则此选项很有用。

<span id="_______-pc______"></span><span id="_______-PC______"></span>**-pc**   
导致命令行的其余部分作为挂起的进程创建的 "隐式命令行" 使用。 如果调试器已连接到具有 "-cimp" 的进程服务器，则使用此命令行。 例如，运行 ```dbgsrv -t <ServerTransport> -pc notepad.exe``` ，然后运行 ```ntsd -premote <Transport> -cimp``` 将导致 ntsd 连接到 dbgsrv 并启动 notepad.exe

<span id="_______-_______"></span> **-?**   
显示包含 DbgSrv 命令行帮助文本的消息框。

有关使用 DbgSrv 的信息，请参阅 [ (用户模式下处理服务器) ](process-servers--user-mode-.md)。

 

 





