---
title: 将 PEB 移出页面时映射符号
description: 将 PEB 移出页面时映射符号
ms.assetid: dba9e686-81fc-4efa-a5c7-293b9e47e0b1
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 720e77a91266fb7589bbaaf383c1b6fd6c361607
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383305"
---
# <a name="mapping-symbols-when-the-peb-is-paged-out"></a>将 PEB 移出页面时映射符号


## <span id="ddk_invalid_or_missing_symbols_dbg"></span><span id="DDK_INVALID_OR_MISSING_SYMBOLS_DBG"></span>


若要加载符号，调试器查看由操作系统加载模块的列表。 指向用户模式下的模块列表的指针是一个进程环境块 (PEB) 中存储的项。

若要回收内存，内存管理器可能会分页出用户模式下的数据，使空间用于其他进程或内核模式组件。 调出的用户模式数据可能包括对 PEB 数据结构。 如果没有此数据结构，调试器无法确定哪些映像加载符号。

**请注意**  这会影响用户模式模块符号文件。 内核模式模块和符号不会影响，因为它们不同的列表中进行跟踪。

 

假设用户模式模块映射到当前进程，并且你想要对其进行了修复符号。 模块的虚拟地址的范围中找到的任何地址。 例如，假设一个模块映射到包含地址 7f78e9e000F 的虚拟地址范围。 输入以下命令。

```dbgcmd
3: kd> !vad 7f78e9e000F 1
```

命令输出会显示有关该模块的虚拟地址说明符 (VAD) 的信息。 命令输出还包括可用于加载模块的符号的重新加载命令字符串。 重新加载命令字符串包含的起始地址 (000007f7\`8e9e0000) 和记事本模块的大小 (32000)。

```dbgcmd
VAD @ fffffa80056fb960
...
Reload command: .reload notepad.exe=000007f7`8e9e0000,32000
```

若要加载符号，请重新加载命令字符串中输入提供的命令。

```dbgcmd
.reload notepad.exe=000007f7`8e9e0000,32000
```

下面是使用稍有不同的方法的另一个示例。 该示例演示如何使用[ **！ vad** ](-vad.md)扩展时 PEB 调出映射符号。基本理念是若要查找的起始地址和相关 DLL 的大小，以便你可以然后使用[ **.reload** ](-reload--reload-module-.md)命令，可以加载必需的符号。 假设当前进程的地址是 0xE0000126\`01BA0AF0 并且想要对其进行了修复符号。 首先，使用[ **！ 过程**](-process.md)命令来获取虚拟地址说明符 (VAD) 根地址：

```dbgcmd
kd> !process e000012601ba0af0 1
PROCESS e000012601ba0af0
    SessionId: 2  Cid: 0b50    Peb: 6fbfffde000  ParentCid: 0efc
    DirBase: 079e8461  ObjectTable: e000000600fbceb0  HandleCount: 360.
    Image: explorer.exe
    VadRoot e000012601a35e70 Vads 201 Clone 0 Private 917. Modified 2198. Locked 0.
...
```

然后，使用[ **！ vad** ](-vad.md)扩展以列出与该进程关联的 VAD 树。 标记为这些 Vad"EXECUTE\_WRITECOPY"属于代码模块。

```dbgcmd
kd> !vad e000012601a35e70
VAD     level      start      end    commit
...
e0000126019f9790 ( 6)      3fff0    3fff7        -1 Private      READONLY
e000012601be1080 ( 7)   37d9bd30 37d9bd3e         2 Mapped  Exe  EXECUTE_WRITECOPY  <-- these are DLLs
e000012600acd970 ( 5)   37d9bec0 37d9bece         2 Mapped  Exe  EXECUTE_WRITECOPY
e000012601a5cba0 ( 7)   37d9c910 37d9c924         2 Mapped  Exe  EXECUTE_WRITECOPY
...
```

然后，使用[ **！ vad** ](-vad.md)再次要查找的起始地址和大小的分页出内存，其中包含所需的 DLL 的扩展名。 这可以确认您已经找到正确的 DLL:

```dbgcmd
kd> !vad e000012601be1080 1

VAD @ e000012601be1080
  Start VPN:      37d9bd30  End VPN: 37d9bd3e  Control Area:  e00001260197b8d0
  First ProtoPte: e0000006013e00a0  Last PTE fffffffffffffffc  Commit Charge         2 (2.)
  Secured.Flink          0  Blink           0  Banked/Extend:        0
  File Offset   0
   ImageMap ViewShare EXECUTE_WRITECOPY

...
        File: \Windows\System32\ExplorerFrame.dll
```

"启动 VPN"字段-在此情况下，0x37D9BD30-指示起始虚拟页码。 这必须转换为真正的地址，通过将其乘以页面大小。 可以使用[ **？（计算表达式）** ](---evaluate-expression-.md)命令以将此值乘以 0x2000，这是页面大小，为基于 Itanium 的计算机的示例来自于。

```dbgcmd
kd> ? 37d9bd3e*2000 
Evaluate expression: 7676040298496 = 000006fb`37a7c000
```

然后该范围的大小可以转换为字节数：

```dbgcmd
kd> ? 37d9bd3e-37d9bd30+1 <--   computes the number of pages
Evaluate expression: 15 = 00000000`0000000f
kd> ? f*2000
Evaluate expression: 122880 = 00000000`0001e000        
```

因此 ExplorerFrame.dll 开始地址 0x000006Fb\`37A7C000，为大型 0x1E000 字节。 您可以加载其符号：

```dbgcmd
kd> .reload /f ExplorerFrame.dll=6fb`37a7c000,1e000
```

 

 





