---
title: 安全模式的功能
description: 安全模式的功能
ms.assetid: bf40d018-7804-47df-9064-fb6f86da4b33
keywords:
- 安全模式，概述
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5d19327f671ac067d8703d8f454b6d4c0b0e3898
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379735"
---
# <a name="features-of-secure-mode"></a>安全模式的功能


## <span id="ddk_features_of_secure_mode_dbg"></span><span id="DDK_FEATURES_OF_SECURE_MODE_DBG"></span>


当安全模式处于活动状态，可用于影响的所有命令*主机*计算机处于非活动状态，并且没有对符号服务器和调试器扩展的一些限制。

安全模式下的特定效果如下所示：

-   [ **.Attach （附加到进程）**](-attach--attach-to-process-.md)， [ **.create （创建过程）**](-create--create-process-.md)， [ **.detach （从分离进程内）**](-detach--detach-from-process-.md)， [ **.abandon （放弃进程）**](-abandon--abandon-process-.md)， [ **.kill （终止进程）**](-kill--kill-process-.md)，[ **.tlist (列表进程 Id)**](-tlist--list-process-ids-.md)， [ **.dump （创建转储文件）**](-dump--create-dump-file-.md)， [ **.opendump (打开转储文件）**](-opendump--open-dump-file-.md)， [ **.writemem （到文件写入内存）**](-writemem--write-memory-to-file-.md)， [ **.netuse （控制网络连接）** ](-netuse--control-network-connections-.md)，并[ **.quit\_（防止意外后退出） 的锁**](-quit-lock--prevent-accidental-quit-.md)命令不可用。

-   [文件 |附加到进程](file---attach-to-a-process.md)，[文件 |打开可执行文件](file---open-executable.md)，[调试 |分离调试对象](debug---detach-debuggee.md)，[调试 |停止调试](debug---stop-debugging.md)，[文件 |打开故障转储](file---open-crash-dump.md)WinDbg 菜单命令不可用。

-   [ **.Shell （命令行界面）** ](-shell--command-shell-.md)命令不可用。

-   必须从本地磁盘; 加载扩展 Dll无法加载它们从 UNC 路径。

-   只能使用两个标准类型的扩展允许使用 Dll （wdbgexts.h 和 dbgeng.h）。 不能作为扩展加载其他类型的 Dll。

-   如果使用的符号服务器，有多个限制。 允许仅 SymSrv (symsrv.dll);服务器 Dll 将不会接受其他符号。 不能为您的符号，使用下游应用商店，将忽略任何现有的下游存储。 不允许 HTTP 和 HTTPS 连接。

已激活后，无法关闭安全模式。 有关详细信息，请参阅[激活安全模式下](activating-secure-mode.md)。

 

 





