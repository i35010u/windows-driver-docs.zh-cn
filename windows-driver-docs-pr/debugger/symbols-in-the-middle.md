---
title: 中间的符号
description: 中间的符号
ms.assetid: 0fbf47fc-1216-4eaa-b4b9-96e206194b54
keywords:
- 第三个计算机上的远程调试，符号
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: c7fe0bc98fe140a1b68a1defb57b61c2c976928e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566071"
---
# <a name="symbols-in-the-middle"></a>中间的符号


## <span id="ddk_symbols_in_the_middle_dbg"></span><span id="DDK_SYMBOLS_IN_THE_MIDDLE_DBG"></span>


在此方案中，有三台计算机。 第一个具有目标应用程序，第二个符号，并且第三个具有该技术人员。

智能客户端的行为类似于常规调试器在每个方法，因为它可以用作调试服务器在同一时间。 这可以链接以及智能客户端在中间的三个计算机。

首先，在计算机上启动的进程服务器\\\\框：

```console
dbgsrv -t npipe:pipe=FarPipe 
```

名为的中间机\\ \\BOXB，两个启动调试器 **-premote**并 **-server**参数。 假设目标应用程序的 PID 为 400 且符号路径为 g:\\MySymbols:

```console
cdb -server npipe:pipe=NearPipe -premote npipe:server=BOXA,pipe=FarPipe -v -y g:\mysymbols -p 400 
```

然后可以按如下所示启动第三台计算机上的调试客户端：

```console
windbg -remote npipe:server=BOXB,pipe=NearPipe 
```

第三台计算机然后用于控制调试，而第二台计算机是实际处理完成和符号进行访问的位置。

 

 





