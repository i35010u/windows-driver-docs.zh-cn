---
title: .dml_flow (Unasemmble 链接)
description: .Dml_flow 命令，将显示反汇编的代码块，并提供可用于构造代码流图形的链接。
ms.assetid: 32B50228-05A5-4BA7-88B1-54D4E502EB85
keywords:
- .dml_flow (Unasemmble 链接) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .dml_flow (Unasemmble with Links)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 46dea3bdf71325eeb3a65621d66fa68aeb98abba
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575187"
---
# <a name="dmlflow-unasemmble-with-links"></a>.dml\_流 (Unasemmble 链接)


**.Dml\_流**命令显示反汇编的代码块，并提供可用于构造代码流图形的链接。

```dbgcmd
.dml_flow Start Target
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="Start"></span><span id="start"></span><span id="START"></span>*启动*  
可以从其达到的目标地址的指令的地址。

<span id="Target"></span><span id="target"></span><span id="TARGET"></span>*Target*  
要拆装的代码块中的地址。

<a name="remarks"></a>备注
-------

请考虑以下示例所示的调用堆栈。

```dbgcmd
0: kd> kL
Child-SP          RetAddr           Call Site
fffff880`0335c688 fffff800`01b41f1c nt!IofCallDriver
fffff880`0335c690 fffff800`01b3b6b4 nt!IoSynchronousPageWrite+0x1cc
fffff880`0335c700 fffff800`01b4195e nt!MiFlushSectionInternal+0x9b8
...
```

假设你想要检查从开头的所有代码路径**nt ！MiFlushSectionInternal**代码块包含返回的地址， `` fffff800`01b3b6b4 ``。 以下命令将获取您入门。

```dbgcmd
.browse .dml_flow nt!MiFlushSectionInternal fffff800`01b3b6b4
```

输出，请在[命令浏览器窗口](command-browser-window.md)，在下图中所示。

![屏幕截图：.dml\-流输出](images/dmlflow01.png)

上图显示了包含目标地址的代码块`` fffff800`01b3b6b4 ``。 还有一个链接 (`` fffff800`01b3b681 ``) 顶部的图像。 它指示存在可从中访问当前代码块只能有一个代码块。 如果单击链接时，将看到代码块拆装，并且您将看到链接，可让您进一步探索代码流图。

在上图底部的两个链接表示两个可从当前代码块访问的代码块。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[调试器标记语言命令](debugger-markup-language-commands.md)

[**如果 （Unasemmble 函数）**](uf--unassemble-function-.md)

 

 






