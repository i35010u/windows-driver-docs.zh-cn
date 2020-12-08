---
title: teb
description: Teb 扩展在线程环境块 (TEB) 中显示信息的格式化视图。
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
ms.openlocfilehash: d02fa8e9912d984632f4878fcf0db76381d7e16c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96830315"
---
# <a name="teb"></a>!teb


**！ Teb** 扩展显示线程环境块 (teb) 中的信息的格式化视图。

```dbgcmd
!teb [TEB-Address] 
```

## <a name="span-idddk__teb_dbgspanspan-idddk__teb_dbgspanparameters"></a><span id="ddk__teb_dbg"></span><span id="DDK__TEB_DBG"></span>参数


<span id="_______TEB-Address______"></span><span id="_______teb-address______"></span><span id="_______TEB-ADDRESS______"></span>*TEB-地址*   
要检查其 TEB 的线程的十六进制地址。  (这不是从线程的内核线程块派生的 TEB 的地址。 ) 如果在用户模式下省略 *TEB* ，则使用当前线程的 TEB。 如果在内核模式下省略此方法，则将显示与当前 [注册上下文](changing-contexts.md#register-context) 相对应的 TEB。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

Exts.dll

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关线程环境块的信息，请参阅 *Microsoft Windows 内部机制* ，标记 Russinovich 和 David 所罗门群岛。

<a name="remarks"></a>备注
-------

TEB 是 Microsoft Windows 线程控制结构的用户模式部分。

如果没有参数的 **！ teb** 扩展在内核模式下出现错误，则应使用 [**！进程**](-process.md) 扩展来确定所需线程的 teb 地址。 请确保将 [注册上下文](changing-contexts.md#register-context) 设置为所需的线程，然后使用 TEB 地址作为 **！ TEB** 的参数。

下面是此命令在用户模式下的输出示例：

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

类似的 [**！ peb**](-peb.md) 扩展显示进程环境块。

 

 





