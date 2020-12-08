---
title: '带链接的 .dml_flow (Unasemmble) '
description: .Dml_flow 命令显示一个反汇编代码块，并提供可用于构造代码流关系图的链接。
keywords:
- 在 Windows 调试) .dml_flow (Unasemmble 与链接
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .dml_flow (Unasemmble with Links)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b930f588215ea63602ccb24530fb32f43037ed42
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96805881"
---
# <a name="dml_flow-unasemmble-with-links"></a>dml \_ flow (带有链接) 的 Unasemmble


**Dml \_ flow** 命令显示一个反汇编代码块，并提供可用于构造代码流关系图的链接。

```dbgcmd
.dml_flow Start Target
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="Start"></span><span id="start"></span><span id="START"></span>*Start*  
可从其访问目标地址的指令的地址。

<span id="Target"></span><span id="target"></span><span id="TARGET"></span>*靶*  
要反汇编的代码块中的地址。

<a name="remarks"></a>备注
-------

请考虑以下示例中所示的调用堆栈。

```dbgcmd
0: kd> kL
Child-SP          RetAddr           Call Site
fffff880`0335c688 fffff800`01b41f1c nt!IofCallDriver
fffff880`0335c690 fffff800`01b3b6b4 nt!IoSynchronousPageWrite+0x1cc
fffff880`0335c700 fffff800`01b4195e nt!MiFlushSectionInternal+0x9b8
...
```

假设您要检查从 nt 开始的所有代码路径 **！MiFlushSectionInternal** 到包含返回地址的代码块 `` fffff800`01b3b6b4 `` 。 以下命令将启动。

```dbgcmd
.browse .dml_flow nt!MiFlushSectionInternal fffff800`01b3b6b4
```

下图显示了 " [命令浏览器" 窗口](command-browser-window.md)中的输出。

![dml 流输出的屏幕截图 \-](images/dmlflow01.png)

上图显示了包含目标地址的代码块 `` fffff800`01b3b6b4 `` 。 图像顶部只有一个链接 (`` fffff800`01b3b681 ``) 。 这表示只有一个代码块可用于访问当前代码块。 如果单击该链接，你将看到代码块反汇编，你将看到使你能够进一步浏览代码流图形的链接。

上图底部的两个链接指示有两个可从当前代码块访问的代码块。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[调试器标记语言命令](debugger-markup-language-commands.md)

[**uf (Unasemmble 函数)**](uf--unassemble-function-.md)

 

 






