---
title: 将虚拟地址转换为物理地址
description: 将虚拟地址转换为物理地址
ms.assetid: 5b3d19df-09cc-4131-ae64-5ce64d986df3
keywords:
- 虚拟地址
- 虚拟地址，将转换为物理地址
- 物理地址
- 物理地址，将从虚拟地址转换
- 地址
- 转换虚拟与物理地址
- 内存，虚拟地址
- 内存中，物理地址
ms.date: 05/04/2018
ms.localizationpriority: medium
ms.openlocfilehash: e870d2322fc236b90131af0ac45166caee44f224
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554951"
---
# <a name="converting-virtual-addresses-to-physical-addresses"></a>将虚拟地址转换为物理地址

## <span id="ddk_converting_virtual_addresses_to_physical_addresses_dbg"></span><span id="DDK_CONVERTING_VIRTUAL_ADDRESSES_TO_PHYSICAL_ADDRESSES_DBG"></span>


大多数调试器命令使用虚拟地址，不是物理地址，作为其输入和输出。 但是，有些时候，具有物理地址很有用。

有两种方法来将虚拟地址转换的物理地址为： 通过使用 **！ vtop**扩展，并通过使用 **！ pte**扩展。

在 Windows 中的虚拟地址的概述，请参阅[虚拟地址空间](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/virtual-address-spaces)。 


### <a name="span-idaddressconversionusingvtopspanspan-idaddressconversionusingvtopspanaddress-conversion-using-vtop"></a><span id="address_conversion_using__vtop"></span><span id="ADDRESS_CONVERSION_USING__VTOP"></span>解决转换使用 ！ vtop

假设你正在调试的目标计算机在其 MyApp.exe 进程正在运行并且你想要调查的虚拟地址 0x0012F980。 下面是可以使用的过程 **！ vtop**扩展来确定相应的物理地址。

**将虚拟地址转换为物理地址使用 ！ vtop**

1.  请确保你正在以十六进制格式。 如果有必要，设置与当前基准[ **N 16** ](n--set-number-base-.md)命令。

2.  确定*字节索引*的地址。 此数字等于最低的 12 位的虚拟地址。 因此，虚拟地址 0x0012F980 具有 0x980 的字节索引。

3.  确定*directory base*使用的地址[ **！ 过程**](-process.md)扩展：

    ```dbgcmd
    kd> !process 0 0
    **** NT ACTIVE PROCESS DUMP ****
    ....
    PROCESS ff779190  SessionId: 0  Cid: 04fc    Peb: 7ffdf000  ParentCid: 0394
     DirBase: 098fd000  ObjectTable: e1646b30  TableSize:   8.
        Image: MyApp.exe
    ```

4.  确定*页上的帧号码*目录基础。 这是只需不带三个尾随十六进制零基目录。 在此示例中，目录基本是 0x098FD000，因此页码帧是 0x098FD。

5.  使用[ **！ vtop** ](-vtop.md)扩展。 此扩展的第一个参数应为页面帧数。 第二个参数 **！ vtop**应为虚拟地址有问题：

    ```dbgcmd
    kd> !vtop 98fd 12f980
    Pdi 0 Pti 12f
    0012f980 09de9000 pfn(09de9)
    ```

    显示的最后一行的第二个数字是开头的物理页的物理地址。

6.  将字节索引添加到网页的开头的地址：0x09DE9000 + 0x980 = 0x09DE9980。 这是所需的物理地址。

你可以验证此计算已正确，可以通过显示在每个地址的内存。 [ **！ D\\**  * ](-db---dc---dd---dp---dq---du---dw.md)扩展显示在指定的物理地址的内存：

```dbgcmd
kd> !dc 9de9980
# 9de9980 6d206e49 726f6d65 00120079 0012f9f4 In memory.......
# 9de9990 0012f9f8 77e57119 77e8e618 ffffffff .....q.w...w....
# 9de99a0 77e727e0 77f6f13e 77f747e0 ffffffff .'.w>..w.G.w....
# 9de99b0 .....
```

[ **D\* （显示内存）** ](d--da--db--dc--dd--dd--df--dp--dq--du--dw--dw--dyb--dyd--display-memor.md)命令使用的虚拟地址作为其参数：

```dbgcmd
kd> dc 12f980
0012f980  6d206e49 726f6d65 00120079 0012f9f4  In memory.......
0012f990  0012f9f8 77e57119 77e8e618 ffffffff  .....q.w...w....
0012f9a0  77e727e0 77f6f13e 77f747e0 ffffffff  .'.w>..w.G.w....
0012f9b0  .....
```

结果是相同的因为这表示，物理地址 0x09DE9980 确实与虚拟地址 0x0012F980 对应。

### <a name="span-idaddressconversionusingptespanspan-idaddressconversionusingptespanaddress-conversion-using-pte"></a><span id="address_conversion_using__pte"></span><span id="ADDRESS_CONVERSION_USING__PTE"></span>解决转换使用 ！ pte

同样，假设你要调查的虚拟地址 0x0012F980 属于 MyApp.exe 进程。 下面是可以使用的过程 **！ pte**扩展来确定相应的物理地址：

**将虚拟地址转换为物理地址使用 ！ pte**

1.  请确保你正在以十六进制格式。 如果有必要，设置与当前基准[ **N 16** ](n--set-number-base-.md)命令。

2.  确定*字节索引*的地址。 此数字等于最低的 12 位的虚拟地址。 因此，虚拟地址 0x0012F980 具有 0x980 的字节索引。

3.  设置[进程上下文](changing-contexts.md#process-context)到所需的进程：

    ```dbgcmd
    kd> !process 0 0
    **** NT ACTIVE PROCESS DUMP ****
    ....
    PROCESS ff779190  SessionId: 0  Cid: 04fc    Peb: 7ffdf000  ParentCid: 0394
        DirBase: 098fd000  ObjectTable: e1646b30  TableSize:   8.
        Image: MyApp.exe

    kd> .process /p ff779190
    Implicit process is now ff779190
    .cache forcedecodeuser done
    ```

4.  使用[ **！ pte** ](-pte.md)扩展名作为其参数的虚拟地址。 这两个列中显示信息。 左侧的列说明了此地址; 页目录项 (PDE)右侧列说明了其页表项 (PTE):

    ```dbgcmd
    kd> !pte 12f980
                   VA 0012f980
    PDE at   C0300000        PTE at C00004BC
    contains 0BA58067      contains 09DE9067
    pfn ba58 ---DA--UWV    pfn 9de9 ---DA--UWV
    ```

5.  查看右侧的列的最后一行。 表示法"pfn 9de9"会显示。 0x9DE9 很*页上的帧号码*(PFN) 的此 PTE。 页面范围数乘以 0x1000 （例如，它保留 12 位的移动）。 结果，0x09DE9000，是开头的网页的物理地址。

6.  将字节索引添加到网页的开头的地址：0x09DE9000 + 0x980 = 0x09DE9980。 这是所需的物理地址。

这是通过先前的方法获取相同的结果。

### <a name="span-idconvertingaddressesbyhandspanspan-idconvertingaddressesbyhandspanconverting-addresses-by-hand"></a><span id="converting_addresses_by_hand"></span><span id="CONVERTING_ADDRESSES_BY_HAND"></span>手动将地址转换

尽管 **！ ptov**并**pte**扩展提供最快的方式将虚拟地址转换为物理地址，可以手动完成此转换。 此过程的说明将您了解某些虚拟内存体系结构的详细信息。

内存中结构大小不同，具体取决于处理器和硬件配置。 此示例摘自 x86 不具有物理地址扩展 (PAE) 启用的系统。

作为虚拟地址再次使用 0x0012F980，首先需要将其转换为二进制文件，手动或使用[ **（显示数字格式） 的.formats** ](-formats--show-number-formats-.md)命令：

```dbgcmd
kd> .formats 12f980
Evaluate expression:
  Hex:     0012f980
  Decimal: 1243520
  Octal:   00004574600
  Binary:  00000000 00010010 11111001 10000000
  Chars:   ....
  Time:    Thu Jan 15 01:25:20 1970
  Float:   low 1.74254e-039 high 0
  Double:  6.14381e-318
```

此虚拟地址是三个字段的组合。 0 到 11 位的字节索引。 Bits 12 到 21 的页表索引。 22 到 31 位都页目录索引。 分隔字段，必须：

```dbgcmd
0x0012F980  =  0y  00000000 00   010010 1111   1001 10000000
```

这会公开的虚拟地址的三个部分：

-   页目录索引 = 0y0000000000 = 0x0

-   页表索引 = 0y0100101111 = 0x12F

-   字节索引 = 0y100110000000 = 0x980

然后，您会为您的系统需要三个条附加信息。

-   每个 PTE 的大小。 这是在非 PAE x86 系统上的 4 个字节。

-   页的大小。 这是 0x1000 字节。

-   PTE\_基虚拟地址。 在非 PAE 系统中，这是 0xC0000000。

使用此数据，可以计算 PTE 本身的地址：

```dbgcmd
PTE address   =   PTE_BASE  
                + (page directory index) * PAGE_SIZE
                + (page table index) * sizeof(MMPTE)
              =   0xc0000000
                + 0x0   * 0x1000
                + 0x12F * 4
              =   0xC00004BC
```

这是将 PTE 的地址。 PTE 是一个 32 位 dword 值。 检查其内容：

```dbgcmd
kd> dd 0xc00004bc L1
c00004bc  09de9067
```

此 PTE 具有 0x09DE9067 的值。 它由两个字段：

-   PTE 的低 12 位均*状态标志*。 在这种情况下，这些标志等于 0x067-或二进制，0y000001100111 中。 状态标志的说明，请参阅[ **！ pte** ](-pte.md)参考页。

-   PTE 的高 20 位均为等于*页上的帧号码*(PFN) 的 PTE。 在这种情况下，PFN 是 0x09DE9。

物理页上的第一个物理地址是 PFN 乘以 0x1000 （移位左 12 位）。 字节索引是在此页上的偏移量。 因此，要查找的物理地址是 0x09DE9000 + 0x980 = 0x09DE9980。 这是由早期方法获取相同的结果。

 

 





