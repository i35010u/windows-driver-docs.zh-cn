---
title: teb
description: Teb 扩展在线程环境块 (TEB) 中显示信息的格式化的的视图。
ms.assetid: 4137b54b-f784-412d-bffd-e8a71a54155e
keywords:
- teb Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- teb
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 1bbfca1dfe2d16695faa052a590706864d8d03ee
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521360"
---
# <a name="teb"></a>!teb


**！ Teb**扩展在线程环境块 (TEB) 中显示的信息的格式化的视图。

```dbgcmd
!teb [TEB-Address] 
```

## <a name="span-idddktebdbgspanspan-idddktebdbgspanparameters"></a><span id="ddk__teb_dbg"></span><span id="DDK__TEB_DBG"></span>参数


<span id="_______TEB-Address______"></span><span id="_______teb-address______"></span><span id="_______TEB-ADDRESS______"></span> *TEB-Address*   
线程想要检查其 TEB 十六进制地址。 （这不是 TEB 如派生自内核线程受阻的线程的地址。）如果*TEB 地址*则使用当前线程在用户模式下，TEB 省略。 如果省略在内核模式下，对应于当前 TEB[注册上下文](changing-contexts.md#register-context)显示。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Exts.dll

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关线程环境块的信息，请参阅*Microsoft Windows Internals*由 Mark Russinovich 和 David solomon 合著。

<a name="remarks"></a>备注
-------

TEB 是 Microsoft Windows 线程控制结构的用户模式部分。

如果 **！ teb**扩展使用没有自变量为你提供错误在内核模式下，应使用[ **！ 过程**](-process.md)扩展来确定所需线程的 TEB 地址。 请确保你[注册上下文](changing-contexts.md#register-context)已设置为所需的线程，然后使用 TEB 地址的参数作为 **！ teb**。

下面是输出的在用户模式下的此命令的示例：

```dbgcmd
0:001> ~
   0  id: 324.458   Suspend: 1 Teb 7ffde000 Unfrozen
.  1  id: 324.48c   Suspend: 1 Teb 7ffdd000 Unfrozen

0:001> !teb 
TEB at 7FFDD000
    ExceptionList:    76ffdc
    Stack Base:       770000
    Stack Limit:      76f000
    SubSystemTib:     0
 FiberData:        1e00
    ArbitraryUser:    0
    Self:             7ffdd000
    EnvironmentPtr:   0
 ClientId:         324.48c
    Real ClientId:    324.48c
    RpcHandle:        0
    Tls Storage:      0
    PEB Address:      7ffdf000
    LastErrorValue:   0
    LastStatusValue:  0
    Count Owned Locks:0
    HardErrorsMode:   0
```

类似[ **！ peb** ](-peb.md)扩展显示进程环境块。

 

 





