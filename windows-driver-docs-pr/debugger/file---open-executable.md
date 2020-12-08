---
title: 文件打开可执行文件
description: 文件打开可执行文件
keywords:
- 文件打开可执行文件
- 启动调试程序，文件打开可执行文件
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 40743caa97a991f2019ae5b35751825a0057462c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96832523"
---
# <a name="file--open-executable"></a>文件 | 打开可执行文件


## <span id="ddk_file_open_executable_dbg"></span><span id="DDK_FILE_OPEN_EXECUTABLE_DBG"></span>


单击 "文件" 菜单上的 "**打开可执行****文件**"，以启动新的用户模式进程并对其进行调试。

此命令等效于按 CTRL + E。 仅当 WinDbg 处于休眠模式时，才能使用此命令。

### <a name="span-iddialog_boxspanspan-iddialog_boxspandialog-box"></a><span id="dialog_box"></span><span id="DIALOG_BOX"></span>对话框

单击 " **打开可执行文件**" 时，将显示 " **打开可执行文件** " 对话框，你可以执行以下操作：

-   在 **"文件名" 框中** 输入可执行文件的完整路径。 或者，您可以使用对话框查找并选择正确的文件。 您必须指定可执行文件的确切路径。 与 "Microsoft Windows **运行** " 对话框和 "命令提示符" 窗口不同，" **打开可执行文件** " 对话框不会搜索当前路径中的可执行文件名称。

-   如果要对可执行文件使用命令行参数，请在 " **自变量** " 框中输入。

-   如果要从默认目录更改起始目录，请在 " **启动目录** " 框中输入目录路径。

-   如果希望 WinDbg 附加到任何 *子进程* (初始目标进程) 启动的其他进程，请选择 " **调试子进程**"。

做出选择后，单击 " **打开**"。

**注意**   使用此命令打开源文件时，会自动将该文件的路径追加到 [源路径](source-path.md)。

 

如果 WinDbg 连接到进程服务器，则无法使用 " **打开可执行文件** " 命令。

### <a name="span-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关启动用于调试的新进程的详细信息和其他方法，请参阅 [使用 WinDbg 调试 User-Mode 进程](debugging-a-user-mode-process-using-windbg.md)。

 

 





