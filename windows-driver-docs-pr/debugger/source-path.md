---
title: 源路径
description: 本主题介绍如何设置源路径或加载单个源代码文件。
ms.assetid: b5dcb557-b413-401a-be4b-2d45b2597e6c
keywords: 源代码文件和路径，源路径
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 686870221ff72a5ecf60cd8a56c18c32bf97302d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527089"
---
# <a name="source-path"></a>源路径


## <span id="ddk_source_path_dbg"></span><span id="DDK_SOURCE_PATH_DBG"></span>


*源路径*指定 C 和 c + + 源文件的位置的目录。

如果你正在调试的可执行文件生成计算机上的用户模式进程和源代码文件仍处于其原始位置，调试器可以自动找到源文件。

在大多数其他情况下，您需要设置的源路径或加载单个源代码文件。

如果所执行[通过在调试器的远程调试](remote-debugging-through-the-debugger.md)，调试服务器使用的源路径。 如果作为调试器使用 WinDbg，每个调试客户端还具有其自己*本地源路径*。 源相关的所有命令都访问本地计算机上的源文件。 您必须在任何客户端或你想要使用的源命令的服务器上设置的正确路径。

此多个路径系统也使调试客户端使用与源相关的命令而无需实际与其他客户端或服务器共享的源文件。 此系统是很有用，如果有私有或机密的源代码文件的用户的一个有权访问。

此外可以在任何时候，而不考虑源路径加载源文件。

### <a name="span-idsourcepathsyntaxspanspan-idsourcepathsyntaxspansource-path-syntax"></a><span id="source_path_syntax"></span><span id="SOURCE_PATH_SYNTAX"></span>源路径语法

调试器的源路径是包含多个目录路径，之间用分号分隔的字符串。

支持相对路径。 但是，除非您始终从相同的目录启动调试器，您应添加驱动器号或网络共享每个路径之前。 此外支持网络共享。

**请注意**如果连接到公司网络，访问源文件的最有效方法是使用源服务器。 还可以通过使用源服务器**srv\\*** 源路径中的字符串。 有关源服务器的详细信息，请参阅[使用源服务器](using-a-source-server.md)。

 

### <a name="span-idcontrollingthesourcepathspanspan-idcontrollingthesourcepathspancontrolling-the-source-path"></a><span id="controlling_the_source_path"></span><span id="CONTROLLING_THE_SOURCE_PATH"></span>控制的源路径

若要控制的源路径和本地源路径，可以执行下列任一操作：

-   启动调试器之前，请使用\_NT\_源\_路径[环境变量](environment-variables.md)若要设置的源路径。 如果尝试添加无效目录通过此环境变量，调试器将忽略此目录。

-   当您启动调试器时，使用 **-srcpath**[命令行选项](command-line-options.md)若要设置的源路径。

-   使用[ **.srcpath （设置源路径）** ](-srcpath---lsrcpath--set-source-path-.md)命令以显示、 设置、 更改或追加到源路径。 如果使用在源服务器[ **.srcfix （使用源服务器）** ](-srcfix---lsrcfix--use-source-server-.md)稍微简单一些。

-   (仅 WinDbg)使用[ **.lsrcpath （设置本地源路径）** ](-srcpath---lsrcpath--set-source-path-.md)命令以显示、 设置、 更改或附加到本地源路径。 如果使用在源服务器[ **.lsrcfix （使用本地源服务器）** ](-srcfix---lsrcfix--use-source-server-.md)稍微简单一些。 此外可以使用参数 lscrpath 使用 WinDbg 命令行。 有关详细信息，请参阅[ **WinDbg 命令行选项**](windbg-command-line-options.md)。

-   (仅 WinDbg)使用[文件 |源文件路径](file---source-file-path.md)命令或按 CTRL + P 以显示，请设置、 更改或将追加到源路径或本地源路径。

可以直接打开或关闭源文件通过执行以下任一操作：

-   使用[ **（加载或卸载源文件） 的 lsf** ](lsf--lsf---load-or-unload-source-file-.md)命令打开或关闭源文件。

-   (仅 WinDbg)使用[ **（打开源文件） 打开**](-open--open-source-file-.md)命令来打开源文件。

-   (仅 WinDbg)使用[文件 | 打开源文件](file---open-source-file.md)命令或按 ctrl + o，若要打开的源文件。 此外可以使用**开放源代码文件 （ctrl + o）** 按钮 (![开放源代码文件按钮的屏幕截图](images/tbopen.png)) 工具栏上。

    **请注意**  当你使用**文件 |打开源文件**（或其快捷菜单或按钮等效项） 若要打开源文件，该文件的路径自动追加到源路径。

     

-   (仅 WinDbg)使用[文件 |最近使用的文件](file---recent-files.md)命令以打开一个在 WinDbg 中最近打开的四个源文件。

-   (仅 WinDbg)使用[文件 |关闭当前窗口](file---close-current-window.md)命令，或单击**关闭**角的按钮[源窗口](source-window.md)关闭源文件。

有关如何使用源代码文件的详细信息，请参阅[在源模式中进行调试](debugging-in-source-mode.md)。

 

 





