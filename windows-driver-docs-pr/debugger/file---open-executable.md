---
title: 文件打开可执行文件
description: 文件打开可执行文件
ms.assetid: dee75298-903d-438f-a66e-fddcfcd74ec7
keywords:
- 文件打开可执行文件
- 正在启动调试器，打开可执行文件的文件
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8be1c3c6bc727afb107cedbbefbce7648a949d67
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56576597"
---
# <a name="file--open-executable"></a>文件 | 打开可执行文件


## <span id="ddk_file_open_executable_dbg"></span><span id="DDK_FILE_OPEN_EXECUTABLE_DBG"></span>


单击**打开可执行文件**上**文件**菜单以启动新的用户模式进程，并对其进行调试。

此命令相当于按下 CTRL + E。 仅当 WinDbg 处于休眠模式时，可以使用此命令。

### <a name="span-iddialogboxspanspan-iddialogboxspandialog-box"></a><span id="dialog_box"></span><span id="DIALOG_BOX"></span>对话框

当您单击**打开可执行文件**，则**打开可执行文件**对话框随即显示，并且您可以执行以下操作：

-   输入中的可执行文件的完整路径**文件名**框。 或者，可以使用对话框的查找并选择适当的文件。 必须指定可执行文件的确切路径。 与 Microsoft Windows 不同**运行**对话框和命令提示符窗口，**打开可执行**对话框不会搜索当前路径的可执行文件的名称。

-   如果你想要使用的可执行文件使用命令行参数，输入中对其**自变量**框。

-   如果你想要更改的开始目录从默认目录中输入该目录路径**开始目录**框。

-   如果你想要附加到任何的 WinDbg*子进程*（其他进程的原始目标进程启动），选择**调试子进程也**。

进行选择后，单击**打开**。

**请注意**  时使用此命令以打开源文件，该文件的路径自动追加到[源路径](source-path.md)。

 

如果 WinDbg 连接到进程服务器，则无法使用**打开可执行文件**命令。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关详细信息和启动新进程以进行调试的其他方法，请参阅[调试用户模式进程使用 WinDbg](debugging-a-user-mode-process-using-windbg.md)。

 

 





