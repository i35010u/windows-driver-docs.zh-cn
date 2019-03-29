---
title: 使用脚本文件
description: 使用脚本文件
ms.assetid: b78a651e-57c8-4863-a8cf-dedd8e308e66
keywords:
- 脚本文件
- 脚本文件概述
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8fad33093eeee4c895bcf2ffdd62dd243c4cdcb5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577548"
---
# <a name="using-script-files"></a>使用脚本文件


## <span id="ddk_using_script_files_dbg"></span><span id="DDK_USING_SCRIPT_FILES_DBG"></span>


一个*脚本文件*是一个文本文件，其中包含一系列调试器命令。 有多种方式调试程序要加载的脚本文件并执行它。 脚本文件可以包含命令按顺序执行，或者可以使用一种更复杂的执行流。

若要执行的脚本文件，可以执行下列任一操作：

-   (KD 和 CDB 仅; 仅当在调试器启动)创建名为 Ntsd.ini 的脚本文件并将其放在其中开始从调试器的目录中。 则调试器将调试程序启动时自动执行此文件。 若要启动的脚本文件使用不同的文件，通过使用指定的路径和文件名称 **-cf** [命令行选项](command-line-options.md)或通过使用**IniFile** 中的条目[Tools.ini](configuring-tools-ini.md)文件。

-   （KD 和 CDB 仅; 当每个会话开始）创建脚本文件并使用指定其路径和文件名称 **-cfr** [命令行选项](command-line-options.md)。 调试器自动执行此脚本文件调试程序启动时和每次重新启动目标的。

-   使用**$ &lt;**， **$ &gt; &lt;**， **$$ &lt;**，和**$$ &gt; &lt;** 命令用于执行脚本文件后运行调试器。 有关语法的详细信息，请参阅[  **$ &lt;，$&gt;&lt;，$&gt;&lt;，$$&gt; &lt; （运行脚本文件）**](-----------------------a---run-script-file-.md).

**$ &gt; &lt;** 并**$$ &gt; &lt;** 命令不同于运行脚本中一个重要的其他方法方法。 使用这些命令，调试器将打开指定的脚本文件、 用分号，替换所有回车和执行单个命令块为生成的文本。 这些命令可用于运行包含调试器命令程序的脚本。 有关这些程序的详细信息，请参阅[使用调试器命令程序](using-debugger-command-programs.md)。X

不能使用仅在 WinDbg 中可用的命令 (如[ **.lsrcfix （使用本地源服务器）**](-srcfix---lsrcfix--use-source-server-.md)， [ **.lsrcpath （设置本地源路径）** ](-srcpath---lsrcpath--set-source-path-.md)， [ **（打开源文件） 打开**](-open--open-source-file-.md)，并且[ **.write\_cmd\_hist （编写命令历史记录）**](-write-cmd-hist--write-command-history-.md)) 脚本文件，即使在 WinDbg 中执行的脚本文件中。 此外，不能使用[ **.beep （扬声器提示音）**](-beep--speaker-beep-.md)， [ **.cls （清除屏幕）**](-cls--clear-screen-.md)， [ **.hh * (打开 HTML 帮助文件）**](-hh--open-html-help-file-.md)， [ **.idle\_cmd （设置空闲命令）**](-idle-cmd--set-idle-command-.md)， [ **.remote (创建 Remote.exeServer)**](-remote--create-remote-exe-server-.md)，内核模式[ **.restart （重新启动内核连接）**](-restart--restart-kernel-connection-.md)，用户模式下[ **.restart （重新启动目标应用程序）**](-restart--restart-target-application-.md)，或[ **.wtitle （设置窗口标题）** ](-wtitle--set-window-title-.md)脚本文件中的命令。

WinDbg 支持相同的脚本作为 KD 和 CDB，有一个小例外。 可以使用[ **.remote\_退出 （退出调试客户端）** ](-remote-exit--exit-debugging-client-.md)命令仅在 KD 或 CDB 使用的脚本文件中。 您不能退出调试客户端但在 WinDbg 中执行的脚本。

 

 





