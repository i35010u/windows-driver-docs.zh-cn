---
title: 两个防火墙
description: 两个防火墙
keywords:
- 远程调试，两个防火墙
- 防火墙和远程调试
ms.date: 06/08/2020
ms.localizationpriority: medium
ms.openlocfilehash: 8f1e3c2a2436c27d9e30a8f44c625b8a42369ea9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803265"
---
# <a name="two-firewalls"></a>两个防火墙

在这种情况下，需要在生成的计算机上执行内核调试。技术人员位于生成 C 中，并有权访问那里的符号。 但是，这两座建筑都具有将不允许传入连接的防火墙。

需要在非特定站点（例如，生成 B）上设置中继器。然后，可以将外部连接到 B，并将 C 连接到 B。

此方案涉及四台计算机：

- 位于构建的中的目标计算机。

- 本地宿主计算机，位于生成。此计算机将运行 KD 连接服务器。 它将通过调试电缆或1394电缆连接到目标计算机，并将向外连接到中继器。 让此计算机的 IP 地址127.0.10.10。

- 构建 B 中的计算机。这将运行中继器。 让其 IP 地址127.0.20.20。

- 技术人员所在的生成 C 中的计算机。 此计算机将运行 WinDbg 作为智能客户端。 让其 IP 地址127.0.30.30。

首先，请确保将目标计算机配置为进行调试，并将其连接到本地主机。 在此示例中，使用了1394电缆。

其次，在127.0.20.20 上启动中继器：

```console
dbengprx -p -s tcp:port=9001 -c tcp:port=9000,clicon=127.0.10.10
```

第三，在生成时在127.0.10.10 上启动 KD 连接服务器，如下所示：

```console
kdsrv -t tcp:port=9000,clicon=127.0.20.20,password=longjump
```

最后，在127.0.30.30 中的 "生成 C" 中启动智能客户端。 (此操作实际上是在生成中启动服务器之前或之后执行的。 ) 

```console
windbg -k kdsrv:server=@{tcp:server=127.0.20.20,port=9001,password=longjump},trans=@{1394:channel=9} -y SymbolPath
```

## <a name="five-computer-scenario"></a>Five-Computer 方案

如果您假设符号在生成 C 中的一台计算机上，但该技术人员在另一台计算机上，则这种情况会更加复杂。

假设127.0.30.30 具有符号（与之前相同），并且其本地名称为 \\ \\ BOXC。 智能客户端可以使用与上述相同的命令来启动，但需要使用附加 **的-server** 参数。 由于没有用户使用此计算机，如果您使用的是 KD 而不是 WinDbg，会占用较少的处理时间：

```console
kd -server npipe:pipe=randomname -k kdsrv:server=@{tcp:server=127.0.20.20,port=9001,password=longjump},trans=@{1394:channel=9} -y SymbolPath
```

然后，技术人员在大楼的其他地方可以启动调试客户端，如下所示：

```console
windbg -remote npipe:server=\\BOXC,pipe=randomname
```

请注意，密码必须由 BOXC) 上的智能客户端 (链中的第一个非中继器提供 \\ \\ ，而不是由链中的最后一个调试器提供。
