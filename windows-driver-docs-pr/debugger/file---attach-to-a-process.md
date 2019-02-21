---
title: 文件附加到进程
description: 文件附加到进程
ms.assetid: 6bd438a3-e9fb-444d-baf6-fffdee0487f2
keywords:
- 文件附加到进程
- 正在启动调试器，文件附加到进程
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: e44f12c5dd1d79fc7133e02c29ef4e0f844e96ea
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56540391"
---
# <a name="file--attach-to-a-process"></a>文件 |附加到进程


## <span id="ddk_file_attach_to_a_process_dbg"></span><span id="DDK_FILE_ATTACH_TO_A_PROCESS_DBG"></span>


单击**附加到进程**上**文件**菜单调试当前正在运行的用户模式应用程序。

此命令相当于按 F6。 仅当 WinDbg 处于休眠模式时，可以使用此命令。

### <a name="span-iddialogboxspanspan-iddialogboxspandialog-box"></a><span id="dialog_box"></span><span id="DIALOG_BOX"></span>对话框

当您单击**附加到进程**，则**附加到进程**对话框随即显示，并且您可以执行以下操作：

- 选择包含正确的进程 ID 和名称的行 (或输入中的进程 ID**进程 ID**框)。
    **请注意**  列出的每个进程具有关联的加号 (**+**)。 可以单击加号以显示有关该进程的命令行、 服务和子进程的信息。

    **请注意**  如果 WinDbg 连接到进程服务器**附加到进程**对话框将显示在远程计算机运行的进程。 进程服务器的详细信息，请参阅[**激活智能客户端**](activating-a-smart-client.md)。

- 如果你想要 noninvasively 附加到进程，请选择**Noninvasive**复选框。

进行选择后，单击**确定**。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关详细信息和附加到进程的其他方法，请参阅[调试用户模式进程使用 WinDbg](debugging-a-user-mode-process-using-windbg.md)并[非侵入调试 （用户模式）](noninvasive-debugging--user-mode-.md)。

 

 





