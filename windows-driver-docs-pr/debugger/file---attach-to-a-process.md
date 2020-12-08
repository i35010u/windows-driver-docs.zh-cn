---
title: 文件附加到进程
description: 文件附加到进程
keywords:
- 文件附加到进程
- 启动调试器，文件附加到进程
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 602ad517171743ae95a5f7d444a7b60b5e72e338
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96825801"
---
# <a name="file--attach-to-a-process"></a>文件 | 附加到进程


## <span id="ddk_file_attach_to_a_process_dbg"></span><span id="DDK_FILE_ATTACH_TO_A_PROCESS_DBG"></span>


单击 "**文件**" 菜单上的 "**附加到进程**" 以调试当前正在运行的用户模式应用程序。

此命令等效于按 F6。 仅当 WinDbg 处于休眠模式时，才能使用此命令。

### <a name="span-iddialog_boxspanspan-iddialog_boxspandialog-box"></a><span id="dialog_box"></span><span id="DIALOG_BOX"></span>对话框

单击 " **附加到进程**" 时，将显示 " **附加到进程** " 对话框，你可以执行以下操作：

- 选择包含正确的进程 ID 和名称的行 (或在 " **进程 id** " 框中输入进程 id) 。
    **注意**  列出的每个进程都有关联的加号 (**+**) 。 可以单击加号以显示有关该进程的命令行、服务和子进程的信息。

    **注意**   如果 WinDbg 连接到进程服务器，则 " **附加到进程** " 对话框将显示远程计算机上运行的进程。 有关进程服务器的详细信息，请参阅 [**激活智能客户端**](activating-a-smart-client.md)。

- 如果要将 noninvasively 附加到进程，请选择 " **Noninvasive** " 复选框。

做出选择后，单击 **"确定"**。

### <a name="span-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关附加到进程的详细信息和其他方法，请参阅 [使用 WinDbg 和 Noninvasive 调试调试 User-Mode 进程](debugging-a-user-mode-process-using-windbg.md) [ (用户模式) ](noninvasive-debugging--user-mode-.md)。

 

 





