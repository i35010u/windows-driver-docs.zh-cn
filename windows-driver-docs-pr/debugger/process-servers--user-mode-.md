---
title: 进程服务器（用户模式）
description: 进程服务器（用户模式）
keywords:
- 通过进程服务器进行远程调试
- 进程服务器
- 进程服务器，概述
- '智能客户端 (用户模式) '
- DbgSrv
- DbgSrv，概述
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3018a8be0acfaa536bfac3a7c2963bf024b14a51
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96829961"
---
# <a name="process-servers-user-mode"></a>进程服务器（用户模式）


## <span id="ddk_process_servers_user_mode__dbg"></span><span id="DDK_PROCESS_SERVERS_USER_MODE__DBG"></span>


通过进程服务器进行远程调试涉及运行服务器计算机上名为 *进程服务器* 的小型应用程序。 然后，在客户端计算机上启动用户模式调试器。 由于此调试器将执行所有实际处理，因此它被称为 *智能客户端*。

用于 Windows 的调试工具包包含一个名为 DbgSrv 的进程服务器 ( # A0) 在用户模式下使用。

这两台计算机不需要运行相同版本的 Windows;它们可以运行任何版本的 Windows。 但是，在客户端上使用的调试器二进制文件和服务器上使用的 DbgSrv 二进制文件必须来自用于 Windows 的调试工具包版本。 此方法不能用于转储文件调试。

若要设置此远程会话，首先设置进程服务器，然后激活智能客户端。 任意数量的智能客户端都可以通过单个进程服务器运行--这些调试会话将保持独立，并且不会相互干扰。 如果调试会话结束，进程服务器将继续运行，并且可用于新的调试会话。

## <a name="span-idin_this_sectionspanin-this-section"></a><span id="in_this_section"></span>本部分中的内容


-   [**激活进程服务器**](activating-a-process-server.md)
-   [**搜索进程服务器**](searching-for-process-servers.md)
-   [**激活智能客户端**](activating-a-smart-client.md)
-   [进程服务器示例](process-server-examples.md)
-   [控制进程服务器会话](controlling-a-process-server-session.md)

 

 





