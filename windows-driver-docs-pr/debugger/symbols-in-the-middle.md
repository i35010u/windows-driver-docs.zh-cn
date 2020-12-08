---
title: 中间的符号
description: 中间的符号
keywords:
- 远程调试，第三台计算机上的符号
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: b26d19578ac1e0044c9c712eabcdc715c1615819
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96825769"
---
# <a name="symbols-in-the-middle"></a>中间的符号


## <span id="ddk_symbols_in_the_middle_dbg"></span><span id="DDK_SYMBOLS_IN_THE_MIDDLE_DBG"></span>


在此方案中，你有三台计算机。 第一个具有目标应用程序，第二个具有符号，第三个包含技术人员。

由于智能客户端的行为方式类似于常规调试器，因此它可以同时用作调试服务器。 这使你可以在中间与智能客户端链接三台计算机。

首先，在计算机 BOXA 上启动进程服务器 \\ \\ ：

```console
dbgsrv -t npipe:pipe=FarPipe 
```

名为 BOXB 的中间计算机 \\ \\ 启动具有 **-premote** 和 **-server** 参数的调试器。 假设目标应用程序的 PID 为400，符号路径为 G： \\ MySymbols：

```console
cdb -server npipe:pipe=NearPipe -premote npipe:server=BOXA,pipe=FarPipe -v -y g:\mysymbols -p 400 
```

然后，可以按如下所示启动第三台计算机上的调试客户端：

```console
windbg -remote npipe:server=BOXB,pipe=NearPipe 
```

然后，第三台计算机用于控制调试，而第二台计算机是完成实际处理并访问符号的位置。

 

 





