---
title: 搜索
description: 搜索扩展在物理内存的指针大小的数据与指定的条件匹配的搜索页。
ms.assetid: 5f9d4e50-c389-4309-8851-0f5069b1b66e
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
ms.openlocfilehash: 893752195106244a17279b41d2f25b6857581f52
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56546001"
---
# <a name="search"></a>！ 搜索


**！ 搜索**扩展在物理内存的指针大小的数据与指定的条件匹配的搜索页。

语法

```dbgcmd
!search [-s] [-p] Data [ Delta [ StartPFN [ EndPFN ]]] 
!search -?
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______-s______"></span><span id="_______-S______"></span> **-s**   
会导致符号检查错误，若要在搜索过程中忽略。 这是很有用，如果您遇到过多"错误的符号的内核"错误。

<span id="_______-p______"></span><span id="_______-P______"></span> **-p**   
值将导致*数据*将被解释为一个 32 位值，防止任何符号扩展。

<span id="_______Data______"></span><span id="_______data______"></span><span id="_______DATA______"></span> *数据*   
指定要搜索的数据。 *数据*必须是目标系统 （32 位或 64 位） 上的指针的大小。 值完全匹配*数据*始终显示。 具体取决于值，还显示其他匹配项*增量*; 请参阅下面备注部分以了解详细信息。

<span id="_______Delta______"></span><span id="_______delta______"></span><span id="_______DELTA______"></span> *Delta*   
指定的值在内存中的值之间允许的偏差*数据*。 请参阅下面备注部分以了解详细信息。

<span id="_______StartPFN______"></span><span id="_______startpfn______"></span><span id="_______STARTPFN______"></span> *StartPFN*   
指定要搜索的范围的开始页码帧 (PFN)。 如果省略此属性，搜索将开始在最低的物理页。

<span id="_______EndPFN______"></span><span id="_______endpfn______"></span><span id="_______ENDPFN______"></span> *EndPFN*   
指定要搜索的范围的结束页码帧 (PFN)。 如果省略此属性，搜索结束从最高的物理页。

<span id="_______-_______"></span> **-?**   
显示此扩展在调试器命令窗口中的帮助。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Kdexts.dll

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

若要显示和搜索的物理内存的更多方法，请参阅[读取和写入内存](reading-and-writing-memory.md)。

<a name="remarks"></a>备注
-------

如果*StartPFN*并*EndPFN*指定，这些以执行所需的开始和范围的结束帧页码为物理内存要在其中搜索。 帧页码的说明，请参阅[转换到物理地址的虚拟地址](converting-virtual-addresses-to-physical-addresses.md)。 如果*StartPFN*并*EndPFN*是省略，则搜索所有的物理内存。

显示所有的命中数。

**！ 搜索**扩展将搜索为指定的页范围内的所有内存，并检查每个 ULONG\_PTR 对齐值。 显示满足以下条件中至少一个的值：

-   值匹配*数据*完全。

-   如果增量是 0 或被省略：值与不同*数据*的单个位。

-   如果增量为非零值：值与不同*数据*由最多*增量*。 换而言之，值介于 2-20 之间\[数据的增量、 数据 + 增量\]。

-   如果增量为非零值：值与不同的单个位的范围 （数据的增量） 中的最小数字。

在大多数情况下，*数据*将指定的地址感兴趣，但任何 ULONG\_可指定 PTR 大小调整数据。

因为搜索所有的内存 （或包含这些结构的任何范围），调试器的搜索引擎结构将驻留在内存中的目标计算机上，你将看到的结构本身的位置的区域中的匹配项。 如果您需要以消除这些匹配项，请执行一个随机值; 如果搜索这将指示调试器的搜索结构的位置。

下面是一些示例。 以下将搜索与 PFN 0x237D 0x80001230 和 0x80001238，非独占之间的值为内存页上：

```dbgcmd
kd> !search 80001234 4 237d 237d 
```

以下将搜索范围为从 PFN 0x2370 到 0x237F 内 0x0F100F0F 的一位的值的内存页。 完全匹配项以粗体形式;其他情况下一个位为关：

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

在显示的列如下所示：**Pfn**是在页的页帧数 (PFN)**偏移量**是该页面; 上的偏移量**命中**是在该地址; 的值**Va**是映射到此物理地址 （如果存在并可确定）; 的虚拟地址**Pte**是页表项 (PTE)。

若要计算的物理地址，将 PFN 保留三个十六进制数字 （12 位），然后加上偏移量。 例如，表中的最后一行是虚拟地址 0x0237D000 + 0x428 = 0x02347D428。

 

 





