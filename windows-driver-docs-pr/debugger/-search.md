---
title: search
description: 搜索扩展会在物理内存中搜索与指定条件匹配的指针大小的数据页。
keywords:
- 搜索 Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- search
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ed3a0d4c9dc8069fabc33e747523aa4b726aa4e4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837565"
---
# <a name="search"></a>!search


**！搜索** 扩展会在物理内存中搜索与指定条件匹配的指针大小的数据页。

语法

```dbgcmd
!search [-s] [-p] Data [ Delta [ StartPFN [ EndPFN ]]] 
!search -?
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______-s______"></span><span id="_______-S______"></span>**-s**   
导致在搜索过程中忽略符号检查错误。 如果获得太多 "内核错误符号" 错误，这很有用。

<span id="_______-p______"></span><span id="_______-P______"></span>**-p**   
导致将 *数据* 的值解释为32位值，从而阻止任何符号扩展。

<span id="_______Data______"></span><span id="_______data______"></span><span id="_______DATA______"></span>*数据*   
指定要搜索的数据。 *数据* 必须是目标系统上的指针的大小 (32 位或64位) 。 始终显示 *数据* 的值的完全匹配项。 还显示其他匹配项，具体取决于 *Delta* 的值;有关详细信息，请参阅下面的 "备注" 部分。

<span id="_______Delta______"></span><span id="_______delta______"></span><span id="_______DELTA______"></span>*增量*   
指定内存中的值与 *数据* 的值之间允许的差异。 有关详细信息，请参阅下面的 "备注" 部分。

<span id="_______StartPFN______"></span><span id="_______startpfn______"></span><span id="_______STARTPFN______"></span>*StartPFN*   
指定要搜索的范围开头 (PFN) 的页面帧号。 如果省略此条件，搜索将从最低的物理页面开始。

<span id="_______EndPFN______"></span><span id="_______endpfn______"></span><span id="_______ENDPFN______"></span>*EndPFN*   
指定要搜索范围末尾 (PFN) 的页帧号。 如果省略此条件，搜索将以最高物理页面结束。

<span id="_______-_______"></span> **-?**   
在调试器中显示此扩展的帮助命令窗口。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

Kdexts.dll

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关显示和搜索物理内存的更多方法，请参阅 [读取和写入内存](reading-and-writing-memory.md)。

<a name="remarks"></a>备注
-------

如果指定了 *StartPFN* 和 *EndPFN* ，则将这些值作为要搜索的物理内存中范围的开始和结束的页面帧号。 有关页帧编号的说明，请参阅 [将虚拟地址转换为物理地址](converting-virtual-addresses-to-physical-addresses.md)。 如果省略了 *StartPFN* 和 *EndPFN* ，则会搜索所有物理内存。

显示所有命中。

**！ Search** 扩展将在指定页面范围内的所有内存中搜索，并检查每个 ULONG \_ PTR 对齐值。 将显示至少满足以下条件之一的值：

-   值与 *数据* 完全匹配。

-   如果 Delta 为0或被省略：值与 *数据* 不同于单个位。

-   如果增量为非零值：值与 *数据* 之间 *的差异最多。* 换句话说，该值位于范围 \[ 数据-Delta、data + Delta 之间 \] 。

-   如果 Delta 为非零值：值不同于范围中的最小数字 (数据增量) 一位。

在大多数情况下， *数据* 将指定您感兴趣的地址，但 \_ 可以指定任何 ULONG PTR 大小的数据。

由于调试器的搜索引擎结构驻留在目标计算机的内存中，因此，如果搜索所有内存 (或包含这些结构的任何范围) 你将在结构本身所在的区域中看到匹配项。 如果需要消除这些匹配项，请搜索随机值;这将指示调试器的搜索结构所在的位置。

下面是一些示例。 以下内容将在 "内存" 页中搜索0x80001230 和0x80001238 之间的值（包括 PFN 0x237D）：

```dbgcmd
kd> !search 80001234 4 237d 237d 
```

以下各项将从 PFN 0x2370 到0x237F 中搜索在一位0x0F100F0F 内的值范围内的内存页。 完全匹配项用粗体指示;其他各项关闭一位：

```dbgcmd
kd> !search 0f100f0f 0 2370 237f
Searching PFNs in range 00002370 - 0000237F for [0F100F0F - 0F100F0F]

Pfn      Offset   Hit      Va       Pte      
- - - - - - - - - - - - - - - - - - -
0000237B 00000368 0F000F0F 01003368 C0004014 
0000237C 00000100 0F100F0F 01004100 C0004014 
0000237D 000003A8 0F100F0F 010053A8 C0004014 
0000237D 000003C8 0F100F8F 010053C8 C0004014 
0000237D 000003E8 0F100F0F 010053E8 C0004014 
0000237D 00000408 0F100F0F 01005408 C0004014 
0000237D 00000428 0F100F8F 01005428 C0004014 
Search done.
```

显示中的列如下所示： **Pfn** 是页面 (Pfn) 页面的帧号; **偏移** 量是该页面上的偏移量; **命中** 是该地址处的值; **Va** 是映射到此物理地址 (的虚拟地址（如果存在），并且可以确定) ; **Pte** 是页表项， (Pte) 。

若要计算物理地址，请将 PFN 左移三个十六进制数字 (12 位) 并添加偏移量。 例如，表中的最后一行是虚拟地址 0x0237D000 + 0x428 = 0x02347D428。

 

 





