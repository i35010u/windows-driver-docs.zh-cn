---
title: 将虚拟地址转换为物理地址
description: 将虚拟地址转换为物理地址
keywords:
- Virtual Address — 虚拟地址
- 虚拟地址，转换为物理地址
- 物理地址
- 物理地址，从虚拟地址转换
- 地址
- 地址，将虚拟转换为物理
- 内存、虚拟地址
- 内存，物理地址
ms.date: 05/04/2018
ms.localizationpriority: medium
ms.openlocfilehash: 51142221ced0dc6be1d464f8cc38b1431ed172de
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838667"
---
# <a name="converting-virtual-addresses-to-physical-addresses"></a>将虚拟地址转换为物理地址

## <span id="ddk_converting_virtual_addresses_to_physical_addresses_dbg"></span><span id="DDK_CONVERTING_VIRTUAL_ADDRESSES_TO_PHYSICAL_ADDRESSES_DBG"></span>


大多数调试器命令使用虚拟地址，而不是物理地址作为其输入和输出。 但有些时候，物理地址可能会很有用。

可以通过两种方式将虚拟地址转换为物理地址：使用 **！ vtop** 扩展，并使用 **！ pte** 扩展。

有关 Windows 中的虚拟地址的概述，请参阅 [虚拟地址空间](../gettingstarted/virtual-address-spaces.md)。 


### <a name="span-idaddress_conversion_using__vtopspanspan-idaddress_conversion_using__vtopspanaddress-conversion-using-vtop"></a><span id="address_conversion_using__vtop"></span><span id="ADDRESS_CONVERSION_USING__VTOP"></span>使用！ vtop 进行地址转换

假设正在调试正在运行 MyApp.exe 进程的目标计算机，并且希望调查虚拟地址0x0012F980。 下面是你将用于 **！ vtop** 扩展的过程，用于确定相应的物理地址。

**使用！ vtop 将虚拟地址转换为物理地址**

1.  请确保使用的是十六进制。 如有必要，请将当前基数设置为 [**N 16**](n--set-number-base-.md) 命令。

2.  确定地址的 *字节索引* 。 此数字等于虚拟地址的最小12位。 因此，虚拟地址0x0012F980 的字节索引为0x980。

3.  使用 [**！ process**](-process.md) extension 确定地址的 *目录基*：

    ```dbgcmd
    kd> !process 0 0
    **** NT ACTIVE PROCESS DUMP ****
    ....
    PROCESS ff779190  SessionId: 0  Cid: 04fc    Peb: 7ffdf000  ParentCid: 0394
     DirBase: 098fd000  ObjectTable: e1646b30  TableSize:   8.
        Image: MyApp.exe
    ```

4.  确定目录基准的 *页面帧号* 。 这只是不带三个尾随十六进制零的目录库。 在此示例中，目录基为0x098FD000，因此页面帧号为0x098FD。

5.  使用 [**！ vtop**](-vtop.md) 扩展。 此扩展插件的第一个参数应为页面帧号。 **！ Vtop** 的第二个参数应是相关的虚拟地址：

    ```dbgcmd
    kd> !vtop 98fd 12f980
    Pdi 0 Pti 12f
    0012f980 09de9000 pfn(09de9)
    ```

    最后一行上显示的第二个数字是物理页开头的物理地址。

6.  将字节索引添加到页面开头的地址： 0x09DE9000 + 0x980 = 0x09DE9980。 这是所需的物理地址。

可以通过在每个地址显示内存来验证是否已正确完成此计算。 [ **！ \\ D** _](-db---dc---dd---dp---dq---du---dw.md)扩展在指定的物理地址显示内存：

```dbgcmd
kd> !dc 9de9980
# 9de9980 6d206e49 726f6d65 00120079 0012f9f4 In memory.......
# 9de9990 0012f9f8 77e57119 77e8e618 ffffffff .....q.w...w....
# 9de99a0 77e727e0 77f6f13e 77f747e0 ffffffff .'.w>..w.G.w....
# 9de99b0 .....
```

[_ *D \* (显示内存)* *](d--da--db--dc--dd--dd--df--dp--dq--du--dw--dw--dyb--dyd--display-memor.md)命令使用虚拟地址作为其参数：

```dbgcmd
kd> dc 12f980
0012f980  6d206e49 726f6d65 00120079 0012f9f4  In memory.......
0012f990  0012f9f8 77e57119 77e8e618 ffffffff  .....q.w...w....
0012f9a0  77e727e0 77f6f13e 77f747e0 ffffffff  .'.w>..w.G.w....
0012f9b0  .....
```

由于结果是相同的，因此这表示物理地址0x09DE9980 确实与虚拟地址0x0012F980 相对应。

### <a name="span-idaddress_conversion_using__ptespanspan-idaddress_conversion_using__ptespanaddress-conversion-using-pte"></a><span id="address_conversion_using__pte"></span><span id="ADDRESS_CONVERSION_USING__PTE"></span>使用！ pte 进行地址转换

同样，假设要调查属于 MyApp.exe 进程的虚拟地址0x0012F980。 下面是你将用于 **！ pte** 扩展的过程，用于确定相应的物理地址：

**使用！ pte 将虚拟地址转换为物理地址**

1.  请确保使用的是十六进制。 如有必要，请将当前基数设置为 [**N 16**](n--set-number-base-.md) 命令。

2.  确定地址的 *字节索引* 。 此数字等于虚拟地址的最小12位。 因此，虚拟地址0x0012F980 的字节索引为0x980。

3.  将 [进程上下文](changing-contexts.md#process-context) 设置为所需的进程：

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

4.  使用带有虚拟地址的 [**！ pte**](-pte.md) 扩展名作为其参数。 这会在两列中显示信息。 左栏描述此地址 (PDE) 的页面目录条目;右列描述了其页面表条目 (PTE) ：

    ```dbgcmd
    kd> !pte 12f980
                   VA 0012f980
    PDE at   C0300000        PTE at C00004BC
    contains 0BA58067      contains 09DE9067
    pfn ba58 ---DA--UWV    pfn 9de9 ---DA--UWV
    ```

5.  查看右侧列的最后一行。 显示 "pfn 9de9" 表示法。 数字0x9DE9 是此 PTE (PFN) 的 *页面帧号* 。 将页面框架数乘以 0x1000 (例如，将其向左移动12位) 。 结果0x09DE9000 是页面开头的物理地址。

6.  将字节索引添加到页面开头的地址： 0x09DE9000 + 0x980 = 0x09DE9980。 这是所需的物理地址。

这与先前的方法获得的结果相同。

### <a name="span-idconverting_addresses_by_handspanspan-idconverting_addresses_by_handspanconverting-addresses-by-hand"></a><span id="converting_addresses_by_hand"></span><span id="CONVERTING_ADDRESSES_BY_HAND"></span>手动转换地址

尽管 **！ ptov** 和 **pte** 扩展提供将虚拟地址转换为物理地址的最快捷方式，但也可以手动执行此转换。 此过程的说明将舍弃虚拟内存体系结构的某些详细信息。

内存结构的大小不同，具体取决于处理器和硬件配置。 此示例取自不具有物理地址扩展 (PAE) 启用的 x86 系统。

再次使用0x0012F980 作为虚拟地址，首先需要将其转换为 binary，无论是手动还是通过使用 [**. 格式 (在) 命令中显示数字格式**](-formats--show-number-formats-.md) ：

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

此虚拟地址是三个字段的组合。 位0到11是字节索引。 位12到21是页表索引。 Bits 22 到31是页目录索引。 分隔字段，就是：

```dbgcmd
0x0012F980  =  0y  00000000 00   010010 1111   1001 10000000
```

这将公开虚拟地址的三个部分：

-   Page directory index = 0y0000000000 = 0x0

-   Page table index = 0y0100101111 = 0x12F

-   Byte index = 0y100110000000 = 0x980

然后，你需要为系统另外另外三条信息。

-   每个 PTE 的大小。 这是非 PAE x86 系统上的4个字节。

-   页面的大小。 这是0x1000 个字节。

-   PTE \_ 基虚拟地址。 在非 PAE 系统上，这是0xC0000000。

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

这是 PTE 的地址。 PTE 为32位 DWORD。 检查其内容：

```dbgcmd
kd> dd 0xc00004bc L1
c00004bc  09de9067
```

此 PTE 的值为0x09DE9067。 它由以下两个字段组成：

-   PTE 的低12位是 *状态标志*。 在这种情况下，这些标志等于 0x067--或 in binary，0y000001100111。 有关状态标志的说明，请参阅 [**！ pte**](-pte.md) 引用页。

-   PTE 的高20位等于) PTE (PFN 的 *页面帧号* 。 在这种情况下，PFN 为0x09DE9。

物理页上的第一个物理地址是 PFN 乘以 0x1000 (向左移动12位) 。 字节索引是此页上的偏移量。 因此，要查找的物理地址为 0x09DE9000 + 0x980 = 0x09DE9980。 这与先前的方法获得的结果相同。

 

