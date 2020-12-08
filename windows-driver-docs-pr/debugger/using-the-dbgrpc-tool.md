---
title: 使用 DbgRpc 工具
description: 使用 DbgRpc 工具
keywords:
- DbgRpc
- DbgRpc，基本用法
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: eb6c676404bfe35e9eb44125d57c8170ba6ab7cc
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803037"
---
# <a name="using-the-dbgrpc-tool"></a>使用 DbgRpc 工具


## <span id="ddk_using_the_dbgrpc_tool_dbg"></span><span id="DDK_USING_THE_DBGRPC_TOOL_DBG"></span>


DbgRpc 工具 ( # A0) 位于适用于 Windows 的调试工具的根目录下，必须在命令提示符窗口中启动。 双击图标不会启动此工具。

必须使用在本地计算机上具有管理权限的帐户或域管理权限运行命令提示符窗口。

DbgRpc 不会调用任何系统服务 (如 LSASS) 。 这使它对于调试非常有用，即使在内核仍在运行的情况下，系统服务也会崩溃。

### <a name="span-idusing_dbgrpc_on_a_remote_computerspanspan-idusing_dbgrpc_on_a_remote_computerspanusing-dbgrpc-on-a-remote-computer"></a><span id="using_dbgrpc_on_a_remote_computer"></span><span id="USING_DBGRPC_ON_A_REMOTE_COMPUTER"></span>在远程计算机上使用 DbgRpc

DbgRpc 也可用于检查来自远程计算机的信息。 为此，远程计算机必须能够接受远程连接并对远程用户进行身份验证。 如果远程计算机的 RPCSS (RPC 终结点映射程序) 服务已崩溃，则 DbgRpc 将无法正常工作。 需要远程计算机上的管理权限或域管理权限。

**-S** 命令行选项用于指定服务器名称， **-p** 参数用于指定传输协议。 TCP 和命名管道协议都可用。 TCP 是推荐的协议;它应该在几乎所有情况下都能正常工作。

以下是示例：

```console
G:\>dbgrpc -s MyServer -p ncacn_ip_tcp -l -P 1e8 -L 0.1
Getting remote cell info ...
Endpoint
Status: Active
Protocol Sequence: LRPC
Endpoint name: OLE18
```

### <a name="span-iddbgrpc_command_linespanspan-iddbgrpc_command_linespandbgrpc-command-line"></a><span id="dbgrpc_command_line"></span><span id="DBGRPC_COMMAND_LINE"></span>DbgRpc 命令行

有关完整命令语法的说明，请参阅 [**DbgRpc Command-Line 选项**](dbgrpc-command-line-options.md)。

 

 





