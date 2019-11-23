---
title: 源路径
description: 本主题介绍如何设置源路径或加载单独的源文件。
ms.assetid: b5dcb557-b413-401a-be4b-2d45b2597e6c
keywords: 源文件和路径，源路径
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 686870221ff72a5ecf60cd8a56c18c32bf97302d
ms.sourcegitcommit: f017184b00f59b088df87a5bd85fec51b7aed8b2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/15/2019
ms.locfileid: "72323596"
---
# <a name="source-path"></a>源路径


## <span id="ddk_source_path_dbg"></span><span id="DDK_SOURCE_PATH_DBG"></span>


*源路径*指定 C 和C++源文件所在的目录。

如果要在生成可执行文件的计算机上调试用户模式进程，并且源文件仍处于其原始位置，则调试器可以自动找到源文件。

在大多数其他情况下，您必须设置源路径或加载单独的源文件。

[通过调试器执行远程调试](remote-debugging-through-the-debugger.md)时，调试服务器使用源路径。 如果使用 WinDbg 作为调试器，则每个调试客户端也有其自己的*本地源路径*。 所有与源相关的命令都访问本地计算机上的源文件。 您必须在要使用源命令的任何客户端或服务器上设置正确的路径。

此多路径系统还允许调试客户端使用源相关的命令，而不会与其他客户端或服务器进行实际共享。 如果有一个用户有权访问的私有或机密源文件，则此系统很有用。

你还可以随时加载源文件，而不考虑源路径。

### <a name="span-idsource_path_syntaxspanspan-idsource_path_syntaxspansource-path-syntax"></a><span id="source_path_syntax"></span><span id="SOURCE_PATH_SYNTAX"></span>源路径语法

调试器的源路径是由多个目录路径组成的字符串，由分号分隔。

支持相对路径。 但是，除非始终从同一目录启动调试器，否则应在每个路径之前添加驱动器号或网络共享。 还支持网络共享。

**注意**  如果已连接到公司网络，则访问源文件的最有效方法是使用源服务器。 您可以通过使用源路径中的**srv\\** * 字符串来使用源服务器。 有关源服务器的详细信息，请参阅[使用源服务器](using-a-source-server.md)。

 

### <a name="span-idcontrolling_the_source_pathspanspan-idcontrolling_the_source_pathspancontrolling-the-source-path"></a><span id="controlling_the_source_path"></span><span id="CONTROLLING_THE_SOURCE_PATH"></span>控制源路径

若要控制源路径和本地源路径，可以执行以下操作之一：

-   在启动调试器之前，请使用 \_NT\_源\_路径[环境变量](environment-variables.md)来设置源路径。 如果尝试通过此环境变量添加无效目录，调试器将忽略此目录。

-   启动调试器时，请使用 **-srcpath**[命令行选项](command-line-options.md)设置源路径。

-   使用 " [**srcpath （设置源路径）** ](-srcpath---lsrcpath--set-source-path-.md) " 命令可显示、设置、更改或追加到源路径。 如果使用源服务器，则[**srcfix （使用源服务器）** ](-srcfix---lsrcfix--use-source-server-.md)会稍微简单一些。

-   （仅限 WinDbg）使用 " [**lsrcpath （设置本地源路径）** ](-srcpath---lsrcpath--set-source-path-.md) " 命令可显示、设置、更改或追加到本地源路径。 如果使用源服务器，则[**lsrcfix （使用本地源服务器）** ](-srcfix---lsrcfix--use-source-server-.md)会稍微简单一些。 你还可以将 WinDbg 命令行与参数-lscrpath 一起使用。 有关详细信息，请参阅[**WinDbg 命令行选项**](windbg-command-line-options.md)。

-   （仅限 WinDbg）使用[文件 |"源文件路径](file---source-file-path.md)" 命令，或按 CTRL + P 显示、设置、更改或追加到源路径或本地源路径。

还可以通过执行下列操作之一来直接打开或关闭源文件：

-   使用[**lsf （加载或卸载源文件）** ](lsf--lsf---load-or-unload-source-file-.md)命令可以打开或关闭源文件。

-   （仅限 WinDbg）使用 "[**打开（打开源文件）** ](-open--open-source-file-.md) " 命令打开一个源文件。

-   （仅限 WinDbg）使用 "[文件" | "打开源文件](file---open-source-file.md)" 命令，或按 ctrl + o 打开一个源文件。 你还可以使用工具栏上的 "打开源文件" **（ctrl + o）** 按钮（![屏幕截图](images/tbopen.png)）。

    **请注意**，在使用**文件 | 时  打开**源文件（或者其快捷菜单或按钮等效项）若要打开源文件，该文件的路径会自动追加到源路径。

     

-   （仅限 WinDbg）使用[文件 |"最近使用的文件](file---recent-files.md)" 命令打开在 WinDbg 中最近打开的四个源文件之一。

-   （仅限 WinDbg）使用[文件 |关闭 "当前窗口](file---close-current-window.md)" 命令，或单击 "[源" 窗口](source-window.md)角的 "**关闭**" 按钮以关闭源文件。

有关如何使用源文件的详细信息，请参阅[在源模式下进行调试](debugging-in-source-mode.md)。

 

 





