---
title: DbgSrv 命令行选项
description: DbgSrv 命令行使用以下语法。
ms.assetid: 817f7ede-bdaf-4d4e-a1bd-579c67ea1ab9
keywords:
- DbgSrv 命令行选项 Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- DbgSrv Command-Line Options
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: fe270ca2f7e6fd79e87f418914becf893ec2c94d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63376092"
---
# <a name="dbgsrv-command-line-options"></a>DbgSrv 命令行选项


DbgSrv 命令行使用以下语法。

```console
dbgsrv -t ServerTransport [-sifeo image.ext] -c[s] AppCmdLine [-x | -pc] 

dbgsrv -? 
```

所有选项都都区分大小写。

## <a name="span-idddkdbgsrvcommandlineoptionsdbgspanspan-idddkdbgsrvcommandlineoptionsdbgspanparameters"></a><span id="ddk_dbgsrv_command_line_options_dbg"></span><span id="DDK_DBGSRV_COMMAND_LINE_OPTIONS_DBG"></span>参数


<span id="_______-t_______ServerTransport______"></span><span id="_______-t_______servertransport______"></span><span id="_______-T_______SERVERTRANSPORT______"></span> **-t** *ServerTransport*   
指定的传输协议。 有关可能的协议列表的语法*服务器传送*每种情况下，请参阅[**激活进程服务器**](activating-a-process-server.md)。

<span id="_______-sifeo_______Executable______"></span><span id="_______-sifeo_______executable______"></span><span id="_______-SIFEO_______EXECUTABLE______"></span> **-sifeo** *可执行文件*   
挂起给定图像的图像文件执行选项 （ifeo 需要） 值。 *可执行文件*应包括可执行映像，包括文件扩展名的文件名称。 -Sifeo 选项允许 DbgSrv 要设置为 ifeo 需要调试程序，以便通过-c 选项，而不会导致递归调用因 ifeo 需要设置而创建的映像。 仅当使用-c，则可以使用此选项。

<span id="_______-c______"></span><span id="_______-C______"></span> **-c**   
若要创建新的进程的原因 DbgSrv。 您可以用于创建你想要调试的进程。 这是类似于从调试器中，生成新的进程的只不过此过程将*不*在创建时进行调试。 若要调试此进程，确定其 PID，并使用 **-p**选项启动智能客户端要调试该进程时。

<span id="_______s______"></span><span id="_______S______"></span> **s**   
将导致新创建过程将立即挂起。 如果使用此选项，则建议作为智能客户端，使用 CDB 和使用-pb 命令行选项，结合使用-p pid 启动智能客户端。 如果包含的命令行上的-pb 选项，该过程将继续进行时将调试器附加到它;否则，您可以恢复与进程[  **~ \*m** ](-m--resume-thread-.md)命令。

<span id="_______AppCmdLine______"></span><span id="_______appcmdline______"></span><span id="_______APPCMDLINE______"></span> *AppCmdLine*   
指定要创建的进程的完整命令行。 *AppCmdLine*可以是 Unicode 或 ASCII 字符串，并且可以包含任何可打印字符。 之后，在出现的所有文本 **-c**\[**s** \]将被参数以便构成的字符串*AppCmdLine*。

<span id="_______-x______"></span><span id="_______-X______"></span> **-x**   
导致要忽略的命令行的其余部分。 此选项非常有用，如果从应用程序可能不需要的文本追加到其命令行启动 DbgSrv。

<span id="_______-pc______"></span><span id="_______-PC______"></span> **-pc**   
导致要忽略的命令行的其余部分。 此选项非常有用，如果从应用程序可能不需要的文本追加到其命令行启动 DbgSrv。 如果 pc DbgSrv 命令行上的最后一个元素会产生语法错误。 除了此限制，pc 是相同的 x。

<span id="_______-_______"></span> **-?**   
显示具有 DbgSrv 命令行帮助文本的消息框。

有关使用 DbgSrv 信息，请参阅[的进程服务器 （用户模式）](process-servers--user-mode-.md)。

 

 





