---
title: 访问全局变量
description: 访问全局变量
ms.assetid: 81daf418-d3cf-413a-8ee0-790b0c0f86c0
keywords:
- 全局变量
- 全局变量，访问
ms.date: 02/20/2020
ms.localizationpriority: medium
ms.openlocfilehash: 2ce50b8367571ea03e4ee718c64b79a112ed71d9
ms.sourcegitcommit: d03c24342b9852013301a37e2ec95592804204f1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/21/2020
ms.locfileid: "77528929"
---
# <a name="accessing-global-variables"></a>访问全局变量


## <span id="ddk_debugging_bios_code_dbg"></span><span id="DDK_DEBUGGING_BIOS_CODE_DBG"></span>


全局变量的名称存储在编译应用程序时创建的符号文件中。 调试器将全局变量的名称解释为虚拟地址。 接受地址作为参数的任何命令也接受变量的名称。 因此，你可以使用 "[按虚拟地址访问内存](accessing-memory-by-virtual-address.md)" 中所述的所有命令来读取或写入全局变量。

此外，还可以使用[ **？（计算表达式）** ](---evaluate-expression-.md)命令显示与任何符号关联的地址。

WinDbg 提供用户界面元素，你可以使用这些元素来查看和编辑全局变量，还可以使用命令。 请参阅[在 WinDbg 中查看和编辑全局变量](viewing-and-editing-global-variables-in-windbg.md)。

请考虑以下示例。 假设要检查 `MyCounter` 全局变量，该变量为32位整数。 还假定默认基数为10。

可以获取此变量的地址，然后按如下所示显示它。

```dbgcmd
0:000> ? MyCounter 
Evaluate expression: 1244892 = 0012fedc
0:000> dd 0x0012fedc L1 
0012fedc  00000052
```

第一个命令输出会告诉您 `MyCounter` 的地址0x0012FEDC。 然后，可以使用[**d\* （显示内存）** ](d--da--db--dc--dd--dd--df--dp--dq--du--dw--dw--dyb--dyd--display-memor.md)命令在此地址显示一个双字。 （也可以使用1244892，这是此地址的十进制版本。 但是，大多数 C 程序员喜欢使用0x0012FEDC。）第二个命令告诉您 MyCounter 的值为0x52 （decimal 82）。

你还可以在下面的命令中执行这些步骤。

```dbgcmd
0:000> dd MyCounter L1 
0012fedc  00000052
```

若要将 `MyCounter` 的值更改为十进制83，请使用以下命令。

```dbgcmd
0:000> ed MyCounter 83 
```

此示例使用 decimal 输入，因为这种格式似乎更适合整数。 但是， [ **d\\** *](d--da--db--dc--dd--dd--df--dp--dq--du--dw--dw--dyb--dyd--display-memor.md)命令的输出仍采用十六进制格式。

```dbgcmd
0:000> dd MyCounter L1 0012fedc  00000053
```

 

 





