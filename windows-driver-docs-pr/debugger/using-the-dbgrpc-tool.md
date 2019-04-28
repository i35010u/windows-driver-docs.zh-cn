---
title: 使用 DbgRpc 工具
description: 使用 DbgRpc 工具
ms.assetid: a98b9141-72e1-4957-a65c-36e677d159a6
keywords:
- DbgRpc
- DbgRpc，基本用法
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 18926641104455df4d8804af9f21ddc0b458cbf3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63340543"
---
# <a name="using-the-dbgrpc-tool"></a>使用 DbgRpc 工具


## <span id="ddk_using_the_dbgrpc_tool_dbg"></span><span id="DDK_USING_THE_DBGRPC_TOOL_DBG"></span>


DbgRpc 工具 (Dbgrpc.exe) 位于根目录下的 Windows 调试工具安装的且必须在命令提示符窗口中启动。 双击该图标不会启动此工具。

必须的帐户下运行命令提示符窗口，本地计算机上具有管理权限或具有域管理权限。

DbgRpc 程序不调用任何系统服务 （例如 LSASS)。 这使其非常适合调试即使系统服务出现故障，只要内核仍在运行。

### <a name="span-idusingdbgrpconaremotecomputerspanspan-idusingdbgrpconaremotecomputerspanusing-dbgrpc-on-a-remote-computer"></a><span id="using_dbgrpc_on_a_remote_computer"></span><span id="USING_DBGRPC_ON_A_REMOTE_COMPUTER"></span>在远程计算机上使用 DbgRpc

DbgRpc 还可用来检查从远程计算机的信息。 为实现此目的，在远程计算机必须能够接受远程连接和远程用户进行身份验证。 如果远程计算机的 RPCSS （RPC 端点映射程序） 服务崩溃，DbgRpc 不能工作。 在远程计算机上的管理或域管理权限是必需的。

**-S**命令行选项用于指定服务器名称，并 **-p**参数用于指定的传输协议。 提供了 TCP 和命名的管道协议。 TCP 是建议的协议;它应在几乎每种情况下工作。

下面是一个示例：

```console
G:\>dbgrpc -s MyServer -p ncacn_ip_tcp -l -P 1e8 -L 0.1
Getting remote cell info ...
Endpoint
Status: Active
Protocol Sequence: LRPC
Endpoint name: OLE18
```

### <a name="span-iddbgrpccommandlinespanspan-iddbgrpccommandlinespandbgrpc-command-line"></a><span id="dbgrpc_command_line"></span><span id="DBGRPC_COMMAND_LINE"></span>DbgRpc 命令行

有关完整的命令语法的说明，请参阅[ **DbgRpc 命令行选项**](dbgrpc-command-line-options.md)。

 

 





