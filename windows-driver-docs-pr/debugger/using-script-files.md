---
title: 使用脚本文件
description: 使用脚本文件
keywords:
- script file
- 脚本文件，概述
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: fe5ebee672e261799902375b6f325a4c2f6c94eb
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803077"
---
# <a name="using-script-files"></a>使用脚本文件


## <span id="ddk_using_script_files_dbg"></span><span id="DDK_USING_SCRIPT_FILES_DBG"></span>


*脚本文件* 是一个文本文件，其中包含一系列调试器命令。 调试器可通过多种方式加载脚本文件并执行该文件。 脚本文件可以包含按顺序执行的命令，也可以使用更复杂的执行流。

若要执行脚本文件，您可以执行下列操作之一：

-   仅 (KD 和 CDB;仅当调试器启动时) 创建一个名为 Ntsd.ini 的脚本文件，并将其放在从中启动调试器的目录中。 调试器在调试器启动时自动执行此文件。 若要为启动脚本文件使用其他文件，请使用 **-cf** [命令行选项](command-line-options.md)或使用 [Tools.ini](configuring-tools-ini.md)文件中的 **IniFile** 条目来指定路径和文件名。

-   仅 (KD 和 CDB;当每个会话启动时) 创建一个脚本文件，并使用 **-cfr** [命令行选项](command-line-options.md)指定其路径和文件名。 调试器启动时和每次重新启动目标时，调试器都会自动执行此脚本文件。

-   使用 **$&lt;** 、 **$&gt;&lt;** 、 **$$&lt;** 和 **$$&gt;&lt;** 命令来执行调试器运行后的脚本文件。 有关语法的详细信息，请参阅 [**$ &lt; ，$ &gt; &lt; ，$ &gt; &lt; ，$ $ &gt; &lt; () 运行脚本文件**](-----------------------a---run-script-file-.md)。

**$&gt;&lt;** 和 **$$&gt;&lt;** 命令在一种重要的方法中不同于运行脚本的其他方法。 使用这些命令时，调试器会打开指定的脚本文件，将所有回车返回替换为分号，并将生成的文本作为单个命令块执行。 这些命令对于运行包含调试器命令程序的脚本很有用。 有关这些程序的详细信息，请参阅 [使用调试器命令程序](using-debugger-command-programs.md)。X-blade

你不能使用仅在 WinDbg (中可用的命令，例如 [**. lsrcfix (使用本地源服务器)**](-srcfix---lsrcfix--use-source-server-.md)， [**. Lsrcpath (设置本地源路径)**](-srcpath---lsrcpath--set-source-path-.md)，， [**打开 (打开的源文件)**](-open--open-source-file-.md)，并写入 cmd 他 (在脚本文件中) [**\_ \_ 写入命令历史记录**](-write-cmd-hist--write-command-history-.md) ，即使脚本文件是在 WinDbg 中执行的。 此外，不能使用 [**。发出嘟嘟声， (扬声器发出嘟嘟声)**](-beep--speaker-beep-.md)， [**cls (清晰的屏幕)**](-cls--clear-screen-.md)， [**Hh (打开 HTML 帮助文件)**](-hh--open-html-help-file-.md) [**。 \_ 空闲 cmd (设置空闲命令**](-idle-cmd--set-idle-command-.md)) ，[**远程 (创建 Remote.exe Server)**](-remote--create-remote-exe-server-.md)、内核模式。重新启动 () 重新启动 [**内核连接**](-restart--restart-kernel-connection-.md) (、用户模式。重新启动) 在脚本文件 [**.wtitle (Set Window Title)**](-wtitle--set-window-title-.md)中重新 [**启动目标应用程序 (**](-restart--restart-target-application-.md)。

WinDbg 支持与 KD 和 CDB 相同的脚本，但有一个小异常。 只能在 KD 或 CDB 使用的脚本文件中使用 [**remote \_ Exit (Exit 调试客户端)**](-remote-exit--exit-debugging-client-.md) 命令。 不能通过在 WinDbg 中执行的脚本从调试客户端退出。

 

 





