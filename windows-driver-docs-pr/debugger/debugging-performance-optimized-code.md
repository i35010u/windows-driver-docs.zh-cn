---
title: 调试性能优化的代码
description: 调试性能优化的代码
keywords:
- 性能优化的代码
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 71dc51ee27f7214975749be689c6237ba52a71c3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96813985"
---
# <a name="debugging-performance-optimized-code"></a>调试性能优化的代码


## <span id="ddk_performance_optimized_code_dbg"></span><span id="DDK_PERFORMANCE_OPTIMIZED_CODE_DBG"></span>


Microsoft 提供了一些方法，用于重新排列编译和链接的代码，使其能够更高效地执行。 这些技术优化内存层次结构的组件，并基于定型方案。

生成的优化可减少分页 (和页错误) ，并增加代码和数据之间的空间位置。 它解决了原始代码的不良位置导致的关键性能瓶颈。 已通过此优化的组件可能会在函数内的代码或数据块移动到二进制文件的不同位置。

在已通过这些技术优化的模块中，代码和数据块的位置通常会位于不同于其在正常编译和链接后所在位置的内存地址。 此外，函数可能已拆分为多个非连续块，以便最常用的代码路径可以在同一页中彼此接近。

因此，函数 (或任何符号) 加上偏移量不一定具有在非优化代码中的相同含义。

### <a name="span-iddebugging_performance_optimized_codespanspan-iddebugging_performance_optimized_codespandebugging-performance-optimized-code"></a><span id="debugging_performance_optimized_code"></span><span id="DEBUGGING_PERFORMANCE_OPTIMIZED_CODE"></span>调试 Performance-Optimized 代码

调试时，可以通过在已加载符号的任何模块上使用 [**！ lmi**](-lmi.md) extension 命令来查看模块是否已进行性能优化：

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

在此输出中，请注意 "特性" 行的术语 " **性能** "。 这表示已将此性能优化应用到 ntdll.dll。

调试器能够理解函数或其他不带偏移量的符号;这允许您在函数或其他标签上设置断点，而不会出现任何问题。 但是，dissassembly 操作的输出可能会造成混淆，因为此反汇编将反映优化器所做的更改。

由于调试器将尝试保持接近原始代码，你可能会看到一些有趣结果。 使用性能优化代码的经验法则只是无法对优化代码执行可靠的地址算法。

以下是示例：

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

你可以从断点列表中看到 **IPTransmit** 的地址为0xF8640CA6。

当你在0xF864B4CB 中 unassemble 此函数中的部分代码时，输出将指示这是超出函数开头的0xE48 字节数。 但是，如果从该地址中减去函数的基，则实际偏移将显示为 "0xA825"。

发生的情况如下：调试器确实显示了从0xF864B4CB 开始的二进制指令的反汇编。 但调试器不是通过简单减法计算偏移量，而是在执行优化之前，调试器会显示与函数项的偏移量相同的偏移量。 该值为0xE48。

另一方面，如果尝试查看 **IPTransmit**+ 0xE48，将看到以下内容：

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

此处的情况是，调试器会将符号 **IPTransmit** 识别为与地址0xF8640CA6 等效，而命令分析器会执行简单的加法操作来查找 0XF8640CA6 + 0XE48 = 0xF8641AEE。 此地址随后用作 [**u (Unassemble)**](u--unassemble-.md) 命令的参数。 但一旦分析此位置，调试器就会发现这不是 **IPTransmit** ，而是0xE48 的偏移量。 事实上，它根本不是此函数的一部分。 相反，它对应于函数 **ARPTransmit** 和0xD8 的偏移量。

出现这种情况的原因是无法通过地址算法来保证性能优化。 尽管调试器可以提取地址并推导出其原始符号和偏移量，但它没有足够的信息来获取符号和偏移量并将其转换为正确的地址。 因此，在这种情况下，反汇编并不有用。

 

 





