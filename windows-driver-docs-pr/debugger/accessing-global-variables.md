---
title: 访问全局变量
description: 访问全局变量
ms.assetid: 81daf418-d3cf-413a-8ee0-790b0c0f86c0
keywords:
- 全局变量
- 全局变量访问
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: f7e736328bc8e355ea75b6da5a87985fa3a48606
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564221"
---
# <a name="accessing-global-variables"></a>访问全局变量


## <span id="ddk_debugging_bios_code_dbg"></span><span id="DDK_DEBUGGING_BIOS_CODE_DBG"></span>


在编译应用程序时创建的符号文件中存储的全局变量的名称。 调试器将解释为一个虚拟地址的全局变量的名称。 此外接受一个地址作为参数的任何命令接受变量的名称。 因此，可以使用的所有命令中所述[访问内存的虚拟地址](accessing-memory-by-virtual-address.md)读取或写入全局变量。

此外，还可以使用[ **？（计算表达式）** ](---evaluate-expression-.md)命令以显示与任何符号相关联的地址。

Visual Studio 和 WinDbg 提供用户界面元素，可以使用 （除了命令） 来查看和编辑全局变量。 请参阅[查看和编辑内存和 Visual Studio 中的寄存器](viewing-memory--variables--and-registers-in-visual-studio.md)并[查看和编辑在 WinDbg 中的全局变量](viewing-and-editing-global-variables-in-windbg.md)。

请考虑下面的示例。 假设你想要检查`MyCounter`全局变量，它是一个 32 位整数。 此外假设默认基数为 10。

可以获取此变量的地址，然后将其显示，如下所示。

```dbgcmd
0:000> ? MyCounter 
Evaluate expression: 1244892 = 0012fedc
0:000> dd 0x0012fedc L1 
0012fedc  00000052
```

第一个命令输出让你知道的地址`MyCounter`是 0x0012FEDC。 然后，可以使用[ **d\* （显示内存）** ](d--da--db--dc--dd--dd--df--dp--dq--du--dw--dw--dyb--dyd--display-memor.md)命令以在此地址显示一个双字。 （您也可以使用 1244892，这是此地址的十进制版本。 但是，大多数 C 程序员更喜欢使用 0x0012FEDC。）第二个命令告知 MyCounter 的值是 0x52 (十进制 82)。

此外可以在以下命令来执行这些步骤。

```dbgcmd
0:000> dd MyCounter L1 
0012fedc  00000052
```

若要更改的值`MyCounter`为十进制 83，使用以下命令。

```dbgcmd
0:000> ed MyCounter 83 
```

此示例使用十进制输入，因为该格式看起来更为自然的整数。 但是的输出[ **d\\**  * ](d--da--db--dc--dd--dd--df--dp--dq--du--dw--dw--dyb--dyd--display-memor.md)命令仍采用十六进制格式。

```dbgcmd
0:000> dd MyCounter L1 0012fedc  00000053
```

 

 





