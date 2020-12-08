---
title: 访问全局变量
description: 访问全局变量
keywords:
- 全局变量
- 全局变量，访问
ms.date: 02/20/2020
ms.localizationpriority: medium
ms.openlocfilehash: cf0abfcc824e68a8ad3a5d8b3b4be3ecf614f329
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96819331"
---
# <a name="accessing-global-variables"></a>访问全局变量


## <span id="ddk_debugging_bios_code_dbg"></span><span id="DDK_DEBUGGING_BIOS_CODE_DBG"></span>


全局变量的名称存储在编译应用程序时创建的符号文件中。 调试器将全局变量的名称解释为虚拟地址。 接受地址作为参数的任何命令也接受变量的名称。 因此，你可以使用 " [按虚拟地址访问内存](accessing-memory-by-virtual-address.md) " 中所述的所有命令来读取或写入全局变量。

此外，还可以使用 [**？ (计算 Expression)**](---evaluate-expression-.md) 命令来显示与任何符号关联的地址。

WinDbg 提供用户界面元素，你可以使用 (，以及) 查看和编辑全局变量的命令。 请参阅 [在 WinDbg 中查看和编辑全局变量](viewing-and-editing-global-variables-in-windbg.md)。

请看下面的示例。 假设要检查 `MyCounter` 全局变量，这是一个32位整数。 还假定默认基数为10。

可以获取此变量的地址，然后按如下所示显示它。

```dbgcmd
0:000> ? MyCounter 
Evaluate expression: 1244892 = 0012fedc
0:000> dd 0x0012fedc L1 
0012fedc  00000052
```

第一个命令输出告诉您的地址 `MyCounter` 为0x0012FEDC。 然后，可以使用 [**d \* (显示内存)**](d--da--db--dc--dd--dd--df--dp--dq--du--dw--dw--dyb--dyd--display-memor.md) 命令在此地址显示一个双字。  (还可以使用1244892，这是此地址的十进制版本。 但是，大多数 C 程序员更喜欢使用0x0012FEDC。 ) 第二个命令告诉您 MyCounter 的值是 0x52 (decimal 82) 。

你还可以在下面的命令中执行这些步骤。

```dbgcmd
0:000> dd MyCounter L1 
0012fedc  00000052
```

若要将的值更改 `MyCounter` 为 decimal 83，请使用以下命令。

```dbgcmd
0:000> ed MyCounter 83 
```

此示例使用 decimal 输入，因为这种格式似乎更适合整数。 但是， [ **d \\** *](d--da--db--dc--dd--dd--df--dp--dq--du--dw--dw--dyb--dyd--display-memor.md)命令的输出仍采用十六进制格式。

```dbgcmd
0:000> dd MyCounter L1 0012fedc  00000053
```

 

 





