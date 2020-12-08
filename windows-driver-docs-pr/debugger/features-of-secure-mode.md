---
title: 安全模式的功能
description: 安全模式的功能
keywords:
- 安全模式，概述
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2ceb67a87f60d44ea891a9093863d023b32e53f7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96828231"
---
# <a name="features-of-secure-mode"></a>安全模式的功能


## <span id="ddk_features_of_secure_mode_dbg"></span><span id="DDK_FEATURES_OF_SECURE_MODE_DBG"></span>


当安全模式处于活动状态时，可用于影响 *主机* 计算机的所有命令都将被停用，并且对符号服务器和调试器扩展存在一些限制。

安全模式的具体效果如下所示：

-   将 [**(附加到进程)**](-attach--attach-to-process-.md)， [**。创建 (创建进程)**](-create--create-process-.md)， [**。分离 (从进程) 分离**](-detach--detach-from-process-.md)， [**(放弃进程)**](-abandon--abandon-process-.md)，，. [**kill (终止进程)**](-kill--kill-process-.md) [**，.**](-opendump--open-dump-file-.md) [**tlist.exe**](-tlist--list-process-ids-.md) () [**(的)**](-dump--create-dump-file-.md) ()  ()  ()  () [****](-writemem--write-memory-to-file-.md) [****](-netuse--control-network-connections-.md) [**\_**](-quit-lock--prevent-accidental-quit-.md)

-   [文件 |附加到进程](file---attach-to-a-process.md)、[文件 |打开可执行文件](file---open-executable.md)，[调试 |分离调试对象](debug---detach-debuggee.md)，[调试 |停止调试](debug---stop-debugging.md)，[文件 |打开故障转储](file---open-crash-dump.md)WinDbg 菜单命令不可用。

-   [**Shell (命令 shell)**](-shell--command-shell-.md)命令不可用。

-   必须从本地磁盘加载扩展 Dll;不能从 UNC 路径加载它们。

-   只允许使用两种标准类型的扩展 Dll (wdbgexts 和 dbgeng) 。 其他类型的 Dll 无法加载为扩展。

-   如果使用的是符号服务器，则有几个限制。 仅允许 SymSrv ( # A0) ;其他符号服务器 Dll 将不被接受。 不能将下游存储用于符号，任何现有的下游存储都将被忽略。 不允许 HTTP 和 HTTPS 连接。

激活后，安全模式将无法关闭。 有关详细信息，请参阅 [激活安全模式](activating-secure-mode.md)。

 

 





