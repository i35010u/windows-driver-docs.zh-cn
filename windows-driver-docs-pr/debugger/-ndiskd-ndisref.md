---
title: ndiskd.ndisref
description: Ndiskd. ndisref 扩展显示跟踪的引用计数的调试日志。
keywords:
- ndiskd ndisref Windows 调试
ms.date: 06/18/2020
topic_type:
- apiref
api_name:
- ndiskd.ndisref
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: d985b49ba08fd59be5905a8eabf3c22d39b0a0e4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96805823"
---
# <a name="ndiskdndisref"></a>!ndiskd.ndisref

**！ Ndiskd ndisref** 扩展显示跟踪的引用计数的调试日志。

```console
!ndiskd.ndisref -handle <x> [-tagtype <str>] [-stacks] [-tag <str>] [-refdebug] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters

<span id="_______-handle______"></span><span id="_______-HANDLE______"></span>*-handle*   
必需。 引用计数块的句柄。

<span id="_______-tagtype______"></span><span id="_______-TAGTYPE______"></span>*-tagtype*   
标记的枚举类型。

<span id="_______-stacks______"></span><span id="_______-STACKS______"></span>*-堆栈*   
包括 (可用的堆栈跟踪) 。

<span id="_______-tag______"></span><span id="_______-TAG______"></span>*-tag*   
限制显示单个标记。

<span id="_______-refdebug______"></span><span id="_______-REFDEBUG______"></span>*-refdebug*   
显示详细的调试日志（如果可用）。

### <a name="dll"></a>DLL

Ndiskd.dll

### <a name="examples"></a>示例

下面的示例将 NDIS 微型端口驱动程序的句柄传递给 **！ ndiskd ndisref** 扩展，以显示该驱动程序的引用计数块。 首先，不使用参数运行 [**！ ndiskd**](-ndiskd-minidriver.md) ，以查看系统上所有微型端口驱动程序的列表。 在下面的示例输出中，查找 kdnic 驱动程序 ffffdf801418d650 的句柄。

```console
3: kd> !ndiskd.minidriver
    ffffdf8015a98380 - tunnel
    ffffdf801418d650 - kdnic
```

使用微型端口驱动程序的句柄输入 **！ ndiskd** 命令，查看此微型端口驱动程序的引用计数块。 下面的示例将引用计数块 excised 的中间部分作为简洁。

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

## <a name="see-also"></a>请参阅

[网络驱动程序设计指南](../network/index.md)

[Windows Vista 和更高版本的网络引用](/windows-hardware/drivers/ddi/_netvista/)

[调试网络堆栈](https://channel9.msdn.com/Shows/Defrag-Tools/Defrag-Tools-175-Debugging-the-Network-Stack)

[**NDIS 扩展 ( # A0)**](ndis-extensions--ndiskd-dll-.md)

[**!ndiskd.help**](-ndiskd-help.md)

[**!ndiskd.minidriver**](-ndiskd-minidriver.md)
