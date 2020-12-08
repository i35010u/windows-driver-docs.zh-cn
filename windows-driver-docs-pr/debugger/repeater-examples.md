---
title: 中继器示例
description: 中继器示例
keywords:
- 中继器，示例
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: f2cdf6f057a64adfdd7803b9577acd0664917d2d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96816939"
---
# <a name="repeater-examples"></a>中继器示例


## <span id="ddk_repeater_examples_dbg"></span><span id="DDK_REPEATER_EXAMPLES_DBG"></span>


假设你有三台计算机、 \\ \\ BOXA、 \\ \\ BOXB 和 \\ \\ BOXC，并且想要将它们分别用作服务器、中继器和客户端。

可以通过以下方式在 BOXA 上启动调试服务器 \\ \\ ：将进程122用作目标：

```console
E:\Debugging Tools for Windows> cdb -server tcp:port=1025,password=wrought -p 122 
```

然后，可以在 BOXB 上启动中继器 \\ \\ ，如下所示：

```console
C:\Misc> dbengprx -c tcp:server=BOXA,port=1025 -s npipe:pipe=MyPipe 
```

最后， \\ 按以下方式在 BOXC 上启动调试客户端 \\ ：

```console
G:\Debugging Tools> windbg -remote npipe:server=BOXB,pipe=MyPipe,password=wrought 
```

以下是另一个示例。 符号位于远程位置127.0.0.30。 因此，你决定在目标为的计算机上使用进程服务器，127.0.0.10。 可以在127.0.0.20 上添加中继器。

你还决定使用反向连接。 首先，在127.0.0.30 上启动客户端：

```console
G:\Debugging Tools> windbg -premote tcp:clicon=127.0.0.20,port=1033 notepad.exe 
```

然后在127.0.0.20 上启动中继器：

```console
C:\Misc> dbengprx -c tcp:clicon=127.0.0.10,port=1025 -s tcp:port=1033,clicon=127.0.0.10 
```

最后，在127.0.0.10 上启动进程服务器：

```console
E:\Debugging Tools for Windows> dbgsrv -t tcp:port=1025,clicon=127.0.0.20 
```

有关使用中继器的更复杂示例，请参阅 [两个防火墙](two-firewalls.md)。

 

 





