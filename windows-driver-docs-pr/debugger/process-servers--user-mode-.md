---
title: 进程服务器 （用户模式）
description: 进程服务器 （用户模式）
ms.assetid: 9391fcd4-c64f-4c2b-89c2-da09be7646d1
keywords:
- 通过进程服务器的远程调试
- 进程服务器
- 进程服务器概述
- 智能客户端 （用户模式）
- DbgSrv
- DbgSrv 概述
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 169761324cce07939590b34ec0e1421d5377b02d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56534579"
---
# <a name="process-servers-user-mode"></a>进程服务器 （用户模式）


## <span id="ddk_process_servers_user_mode__dbg"></span><span id="DDK_PROCESS_SERVERS_USER_MODE__DBG"></span>


通过进程服务器的远程调试涉及到运行名为的小型应用程序*进程服务器*服务器计算机上。 然后客户端计算机上启动用户模式下调试器。 由于此调试器将执行所有实际的处理，调用*智能客户端*。

有关 Windows 调试工具包包括在用户模式下使用名为 DbgSrv (dbgsrv.exe) 的进程服务器。

两台计算机不需要运行相同版本的 Windows;它们可以运行任何版本的 Windows。 但是，客户端上使用的调试程序二进制文件和在服务器上使用 DbgSrv 二进制文件必须来自同一版本的 Windows 调试工具软件包。 此方法不能用于调试转储文件。

若要设置此远程会话，进程服务器设置第一个，并智能客户端激活。 通过一个进程服务器可以运行任意数量的智能客户端--这些调试会话将保持独立，并将不会影响。 如果结束调试会话，进程服务器将继续运行并可用于新的调试会话。

## <a name="span-idinthissectionspanin-this-section"></a><span id="in_this_section"></span>在本部分中


-   [**激活进程服务器**](activating-a-process-server.md)
-   [**搜索的进程服务器**](searching-for-process-servers.md)
-   [**激活智能客户端**](activating-a-smart-client.md)
-   [进程服务器示例](process-server-examples.md)
-   [控制进程服务器会话](controlling-a-process-server-session.md)

 

 





