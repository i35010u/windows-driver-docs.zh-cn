---
title: 启用内核模式转储文件
description: 启用内核模式转储文件
ms.assetid: 4faf389f-764e-4439-9e45-fdd53890b0d1
keywords:
- 转储文件，启用内核模式转储文件
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 10156aa9bda2a55778c0ded4b5ec53f30cbb5e92
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555300"
---
# <a name="enabling-a-kernel-mode-dump-file"></a>启用内核模式转储文件


## <span id="ddk_enabling_a_kernel_mode_dump_file_dbg"></span><span id="DDK_ENABLING_A_KERNEL_MODE_DUMP_FILE_DBG"></span>


在系统崩溃时，Windows 故障转储设置确定是否将创建转储文件，以及如果因此，转储文件的大小将为。

Windows 控制面板控制的内核模式崩溃转储设置。 只有系统管理员可以修改这些设置。

若要更改这些设置，请转到**Control Panel&gt;系统和安全&gt;系统**。 单击**高级系统设置**。 下**启动和恢复**，单击**设置**。

您将看到以下对话框：

![启动和恢复对话框的屏幕截图](images/crashpanel.png)

下**写入调试信息**，可以指定内核模式转储文件设置。 为任何给定的故障，可以创建只有一个转储文件。 请参阅[内核模式转储文件的种类](varieties-of-kernel-mode-dump-files.md)有关不同的转储文件设置的说明。

此外可以选择或取消选中**将事件写入系统日志**并**自动重启**选项。

您选择的设置将应用到任何创建的系统发生崩溃，而不考虑是否意外系统崩溃或是否由调试器的内核模式转储文件。 请参阅[强制系统崩溃](forcing-a-system-crash.md)有关导致有意故障的详细信息。

但是，这些设置不会影响创建的转储文件[ **.dump** ](-dump--create-dump-file-.md)命令。 请参阅[创建转储文件而无需系统崩溃](creating-a-dump-file-without-a-system-crash.md)有关使用此命令的详细信息。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关的主题


[内核模式转储文件](kernel-mode-dump-files.md)

[类型的内核模式转储文件](varieties-of-kernel-mode-dump-files.md)

 

 






