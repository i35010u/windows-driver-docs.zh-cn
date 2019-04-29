---
title: 两个防火墙
description: 两个防火墙
ms.assetid: e6192cf8-02a4-4dbe-8ed7-a64f8efc24f6
keywords:
- 远程调试，两个防火墙
- 防火墙和远程调试
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2c79f520a6a6d767a660fd20c2d4b382eb7b9b9a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380781"
---
# <a name="two-firewalls"></a>两个防火墙


## <span id="ddk_two_firewalls_dbg"></span><span id="DDK_TWO_FIREWALLS_DBG"></span>


在此方案中，您需要执行的内核中构建 A.的计算机上调试在构建 C 中，位于您的技术人员，他或她有权访问符号那里。 但是，这两个建筑物都具有不允许传入连接的防火墙。

需要设置非特定站点-即构建 B.repeater然后可以将外部连接到 B，并连接由里向外 C 到 b。

将有四台计算机在此方案中所涉及：

-   构建 A.中的目标计算机

-   构建 A.中的本地主机计算机此计算机将运行 KD 连接服务器。 它将通过调试电缆或 1394年电缆连接到目标计算机，并将向外连接到 repeater。 允许此计算机的 IP 地址与此 127.0.10.10。

-   构建 B.中的计算机这将运行 repeater。 允许将 127.0.20.20 其 IP 地址。

-   构建 C 技术人员所在的位置中的计算机。 此计算机将充当智能客户端运行 WinDbg。 允许将 127.0.30.30 其 IP 地址。

首先，请确保目标计算机配置用于调试和连接到本地主机计算机。 在此示例中，使用 1394年电缆。

其次，启动 repeater 127.0.20.20 上：

```console
dbengprx -p -s tcp:port=9001 -c tcp:port=9000,clicon=127.0.10.10 
```

第三，启动 KD 连接上的服务器中构建一个 127.0.10.10，如下所示：

```console
kdsrv -t tcp:port=9000,clicon=127.0.20.20,password=longjump 
```

最后，在构建 c 127.0.30.30 上启动智能客户端（这可以实际完成之前或之后在构建 A.启动服务器）

```console
windbg -k kdsrv:server=@{tcp:server=127.0.20.20,port=9001,password=longjump},trans=@{1394:channel=9} -y SymbolPath
```

### <a name="span-idfivecomputerscenariospanspan-idfivecomputerscenariospanfive-computer-scenario"></a><span id="five_computer_scenario"></span><span id="FIVE_COMPUTER_SCENARIO"></span>包含五台计算机方案

如果您假设了构建 C 中的一台计算机上的符号，但该技术人员位于另一台计算机都可以进行这种情况下更加复杂。

假设 127.0.30.30 具有的符号，与之前一样，并且其本地名称是\\ \\BOXC。 可以启动智能客户端，使用与上述相同的命令，但具有附加 **-服务器**参数。 因为没有人将使用此计算机，它需要更少的处理时间，如果你使用而不是 WinDbg KD:

```console
kd -server npipe:pipe=randomname -k kdsrv:server=@{tcp:server=127.0.20.20,port=9001,password=longjump},trans=@{1394:channel=9} -y SymbolPath
```

然后该技术人员构建中的其他位置，可以开始调试客户端，如下所示：

```console
windbg -remote npipe:server=\\BOXC,pipe=randomname 
```

请注意，第一个非-repeater 链中必须提供密码 (上的智能客户端\\ \\BOXC)，而不是链中的最后一个调试器。

 

 





