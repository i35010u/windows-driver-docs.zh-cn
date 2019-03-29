---
title: 调试性能优化的代码
description: 调试性能优化的代码
ms.assetid: 9dbae9e7-c181-491e-9566-6f5e8182aae0
keywords:
- 性能优化的代码
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 37dd60ada9fd9760d1a9b46500e49fab16ac69d1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56563568"
---
# <a name="debugging-performance-optimized-code"></a>调试性能优化的代码


## <span id="ddk_performance_optimized_code_dbg"></span><span id="DDK_PERFORMANCE_OPTIMIZED_CODE_DBG"></span>


Microsoft 拥有某些技术，使用它来重新排列已编译和链接的代码，使它执行与更高的效率。 这些技术优化内存层次结构，该组件，并基于培训方案。

生成优化减少分页 （和页错误），并提高代码和数据之间的空间局部性。 它解决了会通过不佳定位的原始代码中引入的关键性能瓶颈。 已进行过这种优化组件可能具有其代码或数据块函数移到不同位置的二进制文件中。

已经过优化，通过这些技术的模块，在代码和数据块的位置通常将找到的内存地址不同于他们会驻留在普通的编译和链接之后的位置。 此外，函数可能具有已拆分为多个非连续的块，以便最常用的代码路径可以是所在的位置相互靠近相同页面上。

因此，一个函数 （或任何符号） 加上偏移量不一定会会在非优化代码的含义相同。

### <a name="span-iddebuggingperformanceoptimizedcodespanspan-iddebuggingperformanceoptimizedcodespandebugging-performance-optimized-code"></a><span id="debugging_performance_optimized_code"></span><span id="DEBUGGING_PERFORMANCE_OPTIMIZED_CODE"></span>调试性能优化的代码

在调试时，可以看到是否模块已优化性能使用[ **！ lmi** ](-lmi.md)扩展为其加载符号的任何模块的命令：

```dbgcmd
0:000> !lmi ntdll
Loaded Module Info: [ntdll]
         Module: ntdll
   Base Address: 77f80000
     Image Name: ntdll.dll
   Machine Type: 332 (I386)
     Time Stamp: 394193d2 Fri Jun 09 18:03:14 2000
       CheckSum: 861b1
Characteristics: 230e stripped perf
Debug Data Dirs: Type Size     VA  Pointer
                 MISC  110,     0,   76c00 [Data not mapped]
     Image Type: DBG      - Image read successfully from symbol server.
                 c:\symbols\dll\ntdll.dbg
    Symbol Type: DIA PDB  - Symbols loaded successfully from symbol server.
                 c:\symbols\dll\ntdll.pdb
```

在此输出中，请注意，术语**perf** "特征"行上。 这表示，这种性能优化已应用到 ntdll.dll。

调试程序能够了解函数或某一偏移量; 无其他符号这可以在函数或毫无问题的其他标签上设置断点。 但是，拆卸操作的输出可能是令人困惑，因为此反汇编将反映，优化器所做的更改。

由于调试器将尝试保持接近原始代码，可能会看到一些有趣的结果。 法则时使用的性能优化的代码只是您不能对优化的代码执行算术的可靠地址。

下面是一个示例：

```dbgcmd
kd> bl
 0 e f8640ca6     0001 (0001) tcpip!IPTransmit
 1 e f8672660     0001 (0001) tcpip!IPFragment

kd> u f864b4cb
tcpip!IPTransmit+e48:
f864b4cb f3a4             rep     movsb
f864b4cd 8b75cc           mov     esi,[ebp-0x34]
f864b4d0 8b4d10           mov     ecx,[ebp+0x10]
f864b4d3 8b7da4           mov     edi,[ebp-0x5c]
f864b4d6 8bc6             mov     eax,esi
f864b4d8 6a10             push    0x10
f864b4da 034114           add     eax,[ecx+0x14]
f864b4dd 57               push    edi
```

您可以看到从断点列表中的地址**IPTransmit**是 0xF8640CA6。

反汇编 0xF864B4CB 在此函数中的代码部分，输出将指示这是过去的函数的开头 0xE48 字节。 但是，如果减去此地址中的函数的基数，似乎是 0xA825 实际偏移量。

发生了什么情况是：确实，调试器显示开始 0xF864B4CB 的二进制说明反汇编。 但是，而不是通过简单的减法计算偏移量，则调试器会显示-尽它可以-前执行优化的偏移量，因为它在函数进入到存在原始代码中。 该值是 0xE48。

另一方面，如果您尝试一下**IPTransmit**+ 0xE48，就会看到以下：

```dbgcmd
kd> u tcpip!iptransmit+e48
tcpip!ARPTransmit+d8:
f8641aee 0856ff           or      [esi-0x1],dl
f8641af1 75fc             jnz     tcpip!ARPTransmit+0xd9 (f8641aef)
f8641af3 57               push    edi
f8641af4 e828eeffff       call    tcpip!ARPSendData (f8640921)
f8641af9 5f               pop     edi
f8641afa 5e               pop     esi
f8641afb 5b               pop     ebx
f8641afc c9               leave
```

什么这里的问题在于调试器可识别符号**IPTransmit**命令等效于地址 0xF8640CA6，以及分析器执行简单的加法运算，以查找该 0xF8640CA6 + 0xE48 = 0xF8641AEE。 为参数然后使用此地址[ **u （反汇编）** ](u--unassemble-.md)命令。 但在分析此位置后，这不是可发现调试器**IPTransmit** plus 0xE48 的偏移量。 实际上，它根本不属于此函数。 相反，它对应于该函数**ARPTransmit** plus 0xD8 的偏移量。

发生这种情况的原因是该性能优化是不可逆通过算术的地址。 调试器可以接受地址，并推断其原始的符号和偏移量，而它并没有足够的信息获取符号和偏移量并将其转换为正确的地址。 因此，反汇编不在这些情况下很有用。

 

 





