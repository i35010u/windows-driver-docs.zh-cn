---
title: blackboxbsd
description: Blackboxbsd 扩展显示启动状态数据 (BSD) 的辅助启动信息。
keywords:
- blackboxbsd Windows 调试
ms.author: windowsdriverdev
ms.date: 12/06/2018
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
topic_type:
- apiref
api_name:
- blackboxbsd
api_type:
- NA
ms.openlocfilehash: 321b777c3783d71ca12f17851efa2fa1228a6f26
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89217419"
---
# <a name="blackboxbsd"></a>!blackboxbsd

当 **blackboxbsd** 扩展在内核模式转储文件中可用时，它会在 BSD) 信息 (显示缓存的启动状态数据。   从内核模式转储中的缓存数据中检索信息，该转储是在检测到错误时保存的，并且可能并非始终可用。

语法

```dbgcmd
!blackboxbsd  
```

## <a name="span-idparametersspanparameters"></a><span id="Parameters"></span>参数
*无*   


## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

ext.dll


## <a name="span-idremarksspanremarks"></a><span id="Remarks"></span>注释

驱动程序开发人员可以将辅助启动信息添加到转储文件。 驱动程序开发人员 (和 OS) 可以决定何时将此信息添加到转储文件。 这意味着，并非所有内核模式转储文件都包含辅助启动信息。 有关详细信息，请参阅 [编写 Bug 检查原因回调例程](../kernel/writing-a-bug-check-callback-routine.md)。

### <a name="example-command-output"></a>示例命令输出

```dbgcmd
0: kd> !ext.blackboxbsd
Version: 136
Product type: 1

Auto advanced boot: FALSE
Advanced boot menu timeout: 30
Last boot succeeded: TRUE
Last boot shutdown: FALSE
Sleep in progrees: FALSE

Power button timestamp: 0
System running: TRUE
Connected standby in progress: FALSE
User shutdown in progress: FALSE
System shutdown in progress: FALSE
Sleep in progress: 6
Connected standby scenario instance id: 5
Connected standby entry reason: 12
Connected standby exit reason: 31
System sleep transitions to on: 8
Last reference time: 0x1d3645f716b79e3
Last reference time checksum: 0xb6ae84b7
Last update boot id: 6

Boot attempt count: 1
Last boot checkpoint: TRUE
Checksum: 0x7f
Last boot id: 6
Last successful shutdown boot id: 2
Last reported abnormal shutdown boot id: 5

Error info boot id: 0
Error info repeat count: 0
Error info other error count: 0
Error info code: 0
Error info other error count: 0

Power button last press time: 0x1d365b105eb9e3b
Power button cumulative press count: 6
Power button last press boot id: 6
Power button last power watchdog stage: 0x20
Power button watchdog armed: FALSE
Power button shutdown in progress: FALSE
Power button last release time: 0x1d36112993b1191
Power button cumulative release count: 5
Power button last release boot id: 6
Power button error count: 0
Power button current connected standby phase: 1
Power button transition latest checkpoint id: 9
Power button transition latest checkpoint type: 0
Power button transition latest checkpoint sequence number: 77
```

 