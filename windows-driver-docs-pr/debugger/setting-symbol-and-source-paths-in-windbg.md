---
title: 在 WinDbg 中设置符号和可执行映像路径
description: 在 WinDbg 中设置符号和可执行映像路径
ms.assetid: 8EA2509E-0B47-4D28-B934-F1F58F5CFC45
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c945c4d6df1ac25b7be7aaeca7a77d4d25b2c97b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521081"
---
# <a name="setting-symbol-and-executable-image-paths-in-windbg"></a>在 WinDbg 中设置符号和可执行映像路径


## <a name="span-idddksymbolpathdbgspanspan-idddksymbolpathdbgspansymbol-path"></a><span id="ddk_symbol_path_dbg"></span><span id="DDK_SYMBOL_PATH_DBG"></span>符号路径


符号路径指定符号文件的位置的目录。 有关符号和符号文件的详细信息，请参阅[符号](symbols.md)。

**请注意**  如果连接到 Internet 或公司网络，访问符号的最有效方法是使用符号服务器。 您可以使用符号服务器通过使用 srv\*或 symsrv\*符号路径中的字符串。 符号服务器的详细信息，请参阅[符号存储区和符号服务器](symbol-stores-and-symbol-servers.md)。

 

若要控制在 WinDbg 中的符号路径，请执行以下操作：

-   选择**符号文件路径**从**文件**菜单或按 CTRL + S。

-   使用[ **.sympath （设置符号路径）** ](-sympath--set-symbol-path-.md)命令。 如果使用符号服务器， [ **.symfix （设置符号存储区路径）** ](-symfix--set-symbol-store-path-.md)命令相当于 **.sympath** ，但会将你键入。

-   当您启动调试器时，使用 **-y**命令行选项。 请参阅[ **WinDbg 命令行选项**](windbg-command-line-options.md)。

-   启动调试器之前，请使用\_NT\_符号\_路径并\_NT\_ALT\_符号\_路径[环境变量](environment-variables.md)设置路径。 符号路径创建通过追加\_NT\_符号\_后面路径\_NT\_ALT\_符号\_路径。 (通常情况下，将路径设置通过\_NT\_符号\_路径。 但是，你可能想要使用\_NT\_ALT\_符号\_路径重写这些设置，在特殊情况下，例如当你具有共享的符号文件的专用版本。)如果尝试添加无效目录通过这些环境变量，调试器将忽略此目录。

    **请注意**  如果你使用-**sins**命令行选项，调试器会忽略符号路径环境变量。

     

## <a name="span-idexecutableimagepathspanspan-idexecutableimagepathspanspan-idexecutableimagepathspanexecutable-image-path"></a><span id="Executable_Image_Path"></span><span id="executable_image_path"></span><span id="EXECUTABLE_IMAGE_PATH"></span>可执行映像路径


### <span id="ddk_executable_image_path_dbg"></span><span id="DDK_EXECUTABLE_IMAGE_PATH_DBG"></span>

可执行文件是处理器可以运行的二进制文件。 这些文件通常具有.exe、.dll 或.sys 文件扩展名。 可执行文件也称为是模块，尤其是在可执行文件被描述为单位更大的应用程序。 Windows 操作系统运行的可执行文件之前，它将其加载到内存中。 在内存中的可执行文件的副本称为可执行映像或映像。

**请注意**  这些术语有时使用不精确。 例如，某些文档可能会在磁盘上的实际文件使用"映像"。 此外，Windows 内核和 HAL 具有特殊的模块名称。 例如， **nt**模块对应于 Ntoskrnl.exe 文件。

 

可执行映像路径指定二进制可执行文件位于的目录。

在大多数情况下，调试器知道可执行文件的位置，因此不需要设置此文件的路径。

但是，有些情况下需要此路径时。 例如，内核模式[很小的内存转储](small-memory-dump.md)文件不包含所有在停止错误 （即，崩溃） 时存在于内存中的可执行文件。 同样，用户模式的小型转储文件不包含应用程序二进制文件。 如果设置的可执行文件的路径，则调试器可以找到这些二进制文件。

调试器的可执行映像路径是包含多个目录路径，之间用分号分隔的字符串。 支持相对路径。 但是，除非您始终从相同的目录启动调试器，您应添加驱动器号或网络共享每个路径之前。 此外支持网络共享。 调试器搜索可执行映像路径以递归方式。 也就是说，调试器将此路径中搜索列出每个目录的子目录。

若要控制在 WinDbg 中的可执行映像路径，请执行以下操作：

-   选择**图像文件路径**从**文件**菜单中，或按 CTRL + I。

-   使用[ **.exepath （设置可执行文件路径）** ](-exepath--set-executable-path-.md)命令。

-   当您启动调试器时，使用 **-i**命令行选项。 请参阅[ **WinDbg 命令行选项**](windbg-command-line-options.md)。

-   启动调试器之前，请使用\_NT\_可执行文件\_映像\_路径[环境变量](environment-variables.md)设置的路径。

    **请注意**  如果你使用 **-sins**命令行选项，调试器会忽略的可执行映像路径环境变量。

     

 

 





