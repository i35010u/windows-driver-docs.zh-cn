---
title: ndiskd.ndisref
description: Ndiskd.ndisref 扩展显示的跟踪的引用计数的调试日志。
ms.assetid: 6860A567-1017-4184-B8DF-157467360FB9
keywords:
- ndiskd.ndisref Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ndiskd.ndisref
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 23e55a3d327c338fb24340518a700c7697aa1376
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56565824"
---
# <a name="ndiskdndisref"></a>!ndiskd.ndisref


**！ Ndiskd.ndisref**扩展显示的跟踪的引用计数的调试日志。

```console
!ndiskd.ndisref [-handle <x>] [-tagtype <str>] [-stacks] [-tag <str>] [-refdebug] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______-handle______"></span><span id="_______-HANDLE______"></span> *-handle*   
必需。 引用计数块的句柄。

<span id="_______-tagtype______"></span><span id="_______-TAGTYPE______"></span> *-tagtype*   
标记的枚举类型。

<span id="_______-stacks______"></span><span id="_______-STACKS______"></span> *-stacks*   
（如果可用），包括堆栈跟踪。

<span id="_______-tag______"></span><span id="_______-TAG______"></span> *-tag*   
限制到单个标记显示。

<span id="_______-refdebug______"></span><span id="_______-REFDEBUG______"></span> *-refdebug*   
如果可用，则显示详细调试日志。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Ndiskd.dll

<a name="examples"></a>示例
--------

下面的示例将传递到 NDIS 微型端口驱动程序的句柄 **！ ndiskd.ndisref**扩展名，即可显示该驱动程序的引用计数块。 首先，运行[ **！ ndiskd.minidriver** ](-ndiskd-minidriver.md)不带任何参数，以在系统上查看所有微型端口驱动程序的列表。 在下面的示例输出中，查找 kdnic 驱动程序，ffffdf801418d650 的句柄。

```console
3: kd> !ndiskd.minidriver
    ffffdf8015a98380 - tunnel
    ffffdf801418d650 - kdnic
```

使用微型端口驱动程序的句柄，输入 **！ ndiskd.ndisref-处理**命令来查看此微型端口驱动程序的引用计数块。 下面的示例有为简便起见 excised 的引用计数块的中间。

```console
3: kd> !ndiskd.ndisref ffffdf801418d650


REFCOUNT BLOCK

    Tag                                    Number of references                 
    0n0                                    0n6293             Show stacks
    0n1                                    0n1045             Show stacks
    0n2                                    0n4294966717       Show stacks
    0n5                                    0n25048            Show stacks
    0n18                                   0n4294967293       Show stacks
    0n19                                   0n4294967295       Show stacks
    0n21                                   0n4294967036       Show stacks
    0n23                                   0n30818            Show stacks
    0n24                                   0n24693            Show stacks
    0n25                                   0n25808            Show stacks

...

    0n153                                  0n7                Show stacks
    0n154                                  0n3                Show stacks
    0n156                                  0n29972            Show stacks
    0n159                                  0n4294959128       Show stacks
    0n160                                  0n30892            Show stacks
    0n161                                  0n136              Show stacks
    0n162                                  0n4294951910       Show stacks
    0n163                                  0n30892            Show stacks
    0n164                                  0n136              Show stacks
    0n167                                  0n4294965996       Show stacks

    Include inactive tags
```

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[网络驱动程序设计指南](https://msdn.microsoft.com/windows/hardware/drivers/network/index)

[Windows Vista 和更高版本的网络参考](https://msdn.microsoft.com/library/windows/hardware/ff571081)

[调试网络堆栈](https://go.microsoft.com/fwlink/p/?linkid=845311)

[**NDIS 扩展 (Ndiskd.dll)**](ndis-extensions--ndiskd-dll-.md)

[**!ndiskd.help**](-ndiskd-help.md)

[**!ndiskd.minidriver**](-ndiskd-minidriver.md)

 

 






