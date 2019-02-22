---
title: Repeater 示例
description: Repeater 示例
ms.assetid: 83aff647-65a7-409f-adce-254305395775
keywords:
- repeater 示例
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9a6dc91c7ba60ab880546da6fd293e7846c1d1ec
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542245"
---
# <a name="repeater-examples"></a>Repeater 示例


## <span id="ddk_repeater_examples_dbg"></span><span id="DDK_REPEATER_EXAMPLES_DBG"></span>


让我们假设您有三个计算机\\\\框中， \\ \\BOXB，和\\ \\BOXC，并且您想要分别为服务器、 repeater 和客户端，使用它们。

你可以开始调试服务器上\\\\框，按以下方式使用作为目标，122 过程：

```console
E:\Debugging Tools for Windows> cdb -server tcp:port=1025,password=wrought -p 122 
```

你可以在将启动 repeater \\ \\BOXB，如下所示：

```console
C:\Misc> dbengprx -c tcp:server=BOXA,port=1025 -s npipe:pipe=MyPipe 
```

最后，在开始调试客户端\\ \\BOXC 按以下方式：

```console
G:\Debugging Tools> windbg -remote npipe:server=BOXB,pipe=MyPipe,password=wrought 
```

下面是另一个示例。 在远程位置 127.0.0.30 是您自己的符号。 因此您决定使用目标的位置，127.0.0.10 在计算机上的进程服务器。 Repeater 置于 127.0.0.20。

您还决定使用反向连接。 因此在开始通过 127.0.0.30 上启动客户端：

```console
G:\Debugging Tools> windbg -premote tcp:clicon=127.0.0.20,port=1033 notepad.exe 
```

然后启动 repeater 127.0.0.20 上：

```console
C:\Misc> dbengprx -c tcp:clicon=127.0.0.10,port=1025 -s tcp:port=1033,clicon=127.0.0.10 
```

和最后 127.0.0.10 上启动进程服务器：

```console
E:\Debugging Tools for Windows> dbgsrv -t tcp:port=1025,clicon=127.0.0.20 
```

有关更复杂的示例使用重复字符，请参阅[两个防火墙](two-firewalls.md)。

 

 





