---
title: 在 CDB 中设置符号和可执行映像路径
description: 在 CDB 中设置符号和可执行映像路径
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4fbb78efcce02c4e6521fc0cf535b8d6bc7555e3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96829711"
---
# <a name="setting-symbol-and-executable-image-paths-in-cdb"></a>在 CDB 中设置符号和可执行映像路径


## <a name="span-idddk_symbol_path_dbgspanspan-idddk_symbol_path_dbgspansymbol-path"></a><span id="ddk_symbol_path_dbg"></span><span id="DDK_SYMBOL_PATH_DBG"></span>符号路径


符号路径指定符号文件所在的目录。 有关符号和符号文件的详细信息，请参阅 [符号](symbols.md)。

**注意**   如果已连接到 Internet 或企业网络，则访问符号的最有效方法是使用符号服务器。 您可以通过使用符号 \* 路径中的 srv 或 symsrv 字符串来使用符号服务器 \* 。 有关符号服务器的详细信息，请参阅 [符号存储和符号服务器](symbol-stores-and-symbol-servers.md)。

 

若要控制 CDB 中的符号路径，请执行以下操作之一：

-   输入 [**sympath (设置符号路径)**](-sympath--set-symbol-path-.md) 命令。 如果使用的是符号服务器，则 [**symfix (设置符号存储路径)**](-symfix--set-symbol-store-path-.md) 命令类似于. sympath，但会保存键入内容。

-   启动调试器时，请使用 **-y** 命令行选项。 请参阅 [**CDB Command-Line 选项**](cdb-command-line-options.md)。

-   在启动调试器之前，请使用 \_ nt \_ 符号 \_ 路径和 \_ nt \_ ALT \_ 符号 \_ 路径 [环境变量](environment-variables.md) 来设置路径。 符号路径是通过 \_ \_ \_ 在 \_ nt \_ ALT \_ 符号路径后面追加 nt 符号路径来创建的 \_ 。  (通常会通过 \_ NT \_ 符号路径设置路径 \_ 。 但是， \_ \_ 在特殊情况下，你可能希望使用 NT ALT \_ 符号 \_ 路径来替代这些设置，例如，当你拥有共享符号文件的专用版本时。 ) 

    **注意**  如果使用 **-问题** 命令行选项，调试器将忽略符号路径环境变量。

     

## <a name="span-idexecutable_image_pathspanspan-idexecutable_image_pathspanspan-idexecutable_image_pathspanexecutable-image-path"></a><span id="Executable_Image_Path"></span><span id="executable_image_path"></span><span id="EXECUTABLE_IMAGE_PATH"></span>可执行映像路径


### <span id="ddk_executable_image_path_dbg"></span><span id="DDK_EXECUTABLE_IMAGE_PATH_DBG"></span>

可执行文件是处理器可以运行的二进制文件。 这些文件通常具有 .exe、.dll 或 .sys 文件扩展名。 可执行文件也称为模块，尤其是在将可执行文件描述为更大的应用程序的单元时。 在 Windows 操作系统运行可执行文件之前，它会将其加载到内存中。 内存中的可执行文件的副本称为可执行映像或映像。

**注意**   这些术语有时 imprecisely 使用。 例如，某些文档可能会对磁盘上的实际文件使用 "image"。 此外，Windows 内核和 HAL 具有特殊的模块名称。 例如， **nt** 模块与 Ntoskrnl.exe 文件相对应。

 

可执行映像路径指定二进制可执行文件所在的目录。

在大多数情况下，调试器知道可执行文件的位置，因此您不必为此文件设置路径。

但是，在某些情况下，此路径是必需的。 例如，内核模式 [小内存转储](small-memory-dump.md) 文件不包含出现停止错误时内存中存在的所有可执行文件 (即，崩溃) 。 同样，用户模式小型转储文件不包含应用程序二进制文件。 如果设置可执行文件的路径，则调试器可以找到这些二进制文件。

调试器的可执行映像路径是由多个目录路径组成的字符串，由分号分隔。 支持相对路径。 但是，除非始终从同一目录启动调试器，否则应在每个路径之前添加驱动器号或网络共享。 还支持网络共享。 调试器会以递归方式搜索可执行图像路径。 也就是说，调试器会搜索此路径中列出的每个目录的子目录。

若要控制 CDB 中的可执行映像路径，请执行以下操作之一：

-   输入 [**exepath (设置可执行文件路径)**](-exepath--set-executable-path-.md) 命令。

-   启动调试器时，使用 **-i** 命令行选项。 请参阅 [**CDB Command-Line 选项**](cdb-command-line-options.md)。

-   在启动调试器之前，请使用 \_ NT \_ 可执行文件 \_ 映像 \_ 路径 [环境变量](environment-variables.md) 来设置路径。

    **注意**  如果使用 **-问题** 命令行选项，调试器将忽略可执行映像路径环境变量。

     

 

 





