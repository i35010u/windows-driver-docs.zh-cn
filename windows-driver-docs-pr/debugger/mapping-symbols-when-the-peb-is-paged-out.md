---
title: 将 PEB 移出页面时映射符号
description: 将 PEB 移出页面时映射符号
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6d3af948498825c52cc86c52541a28613e849a45
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96814535"
---
# <a name="mapping-symbols-when-the-peb-is-paged-out"></a>将 PEB 移出页面时映射符号


## <span id="ddk_invalid_or_missing_symbols_dbg"></span><span id="DDK_INVALID_OR_MISSING_SYMBOLS_DBG"></span>


若要加载符号，调试器会查看操作系统加载的模块的列表。 指向用户模式模块列表的指针是存储在进程环境块 (PEB) 中的项之一。

为了回收内存，内存管理器可能会分页输出用户模式数据，为其他进程或内核模式组件腾出空间。 已分页的用户模式数据可能包括 PEB 数据结构。 如果没有此数据结构，调试器无法确定要为哪些图像加载符号。

**注意**   这会影响仅适用于用户模式模块的符号文件。 内核模式模块和符号不受影响，因为它们是在其他列表中跟踪的。

 

假设用户模式模块映射到当前进程，并且你想要为其修复符号。 查找模块的虚拟地址范围中的任何地址。 例如，假设某个模块映射到一个包含地址7f78e9e000F 的虚拟地址范围。 输入以下命令。

```dbgcmd
3: kd> !vad 7f78e9e000F 1
```

命令输出显示有关该模块的虚拟地址描述符 (VAD) 的信息。 命令输出还包括一个可用于加载模块符号的重载命令字符串。 重载命令字符串包括 000007f7 8e9e0000 的起始地址 (\` "记事本" 模块) 和大小 (32000) 。

```dbgcmd
VAD @ fffffa80056fb960
...
Reload command: .reload notepad.exe=000007f7`8e9e0000,32000
```

若要加载符号，请输入 "重载命令字符串" 中提供的命令。

```dbgcmd
.reload notepad.exe=000007f7`8e9e0000,32000
```

下面是另一个使用略微不同的方法的示例。 该示例演示如何使用 [**！ vad**](-vad.md) 扩展在 PEB 被分页时映射符号。基本思路是查找相关 DLL 的起始地址和大小，以便可以使用 [**reload.sql**](-reload--reload-module-.md) 命令加载所需的符号。 假设当前进程的地址是 0xE0000126 \` 01BA0AF0，并且你想要为其修复符号。 首先，使用 [**！ process**](-process.md) 命令获取虚拟地址描述符 (VAD) 根地址：

```dbgcmd
kd> !process e000012601ba0af0 1
PROCESS e000012601ba0af0
    SessionId: 2  Cid: 0b50    Peb: 6fbfffde000  ParentCid: 0efc
    DirBase: 079e8461  ObjectTable: e000000600fbceb0  HandleCount: 360.
    Image: explorer.exe
    VadRoot e000012601a35e70 Vads 201 Clone 0 Private 917. Modified 2198. Locked 0.
...
```

然后，使用 [**！ vad**](-vad.md) 扩展列出与进程关联的 vad 树。 标记为 "EXECUTE \_ WRITECOPY" 的 vad 属于代码模块。

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

然后，再次使用 [**！ vad**](-vad.md) 扩展来查找已分页的内存（包含相关 DLL）的起始地址和大小。 这会确认已找到正确的 DLL：

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

"启动 VPN" 字段（在本例中为0x37D9BD30）表示起始虚拟页码。 此值必须转换为实际地址，方法是将其与页面大小相乘。 您可以使用 " [**？ (评估 Expression)**](---evaluate-expression-.md) 命令将此值与0x2000 相乘，这是该示例所源自的基于 Itanium 的计算机的页面大小。

```dbgcmd
kd> ? 37d9bd3e*2000 
Evaluate expression: 7676040298496 = 000006fb`37a7c000
```

然后，可以将范围的大小转换为字节：

```dbgcmd
kd> ? 37d9bd3e-37d9bd30+1 <--   computes the number of pages
Evaluate expression: 15 = 00000000`0000000f
kd> ? f*2000
Evaluate expression: 122880 = 00000000`0001e000        
```

因此 ExplorerFrame.dll 从地址 0x000006Fb \` 37A7C000 开始，并且为0x1E000 字节。 可以通过加载其符号：

```dbgcmd
kd> .reload /f ExplorerFrame.dll=6fb`37a7c000,1e000
```

 

 





