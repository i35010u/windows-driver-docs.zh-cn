---
title: smt
description: Smt 扩展显示的同时进行多线程的处理器信息的摘要。
ms.assetid: 28c07f89-6208-4b04-b7b9-825dda4f5f5a
keywords:
- smt Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- smt
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 803bdeef549c43d9932421871e25246706595c5f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63339777"
---
# <a name="smt"></a>!smt


**！ Smt**扩展显示的同时进行多线程的处理器信息的摘要。

```dbgcmd
!smt
```

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>不可用</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 及更高版本</strong></p></td>
<td align="left"><p>Kdexts.dll</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

下面是一个示例：

```dbgcmd
lkd> !smt 
SMT Summary:
------------
   KeActiveProcessors: **------------------------------ (00000003)
        KiIdleSummary: -------------------------------- (00000000)
 No PRCB     Set Master SMT Set                                     IAID
  0 820f4820 Master     **------------------------------ (00000003)  00
  1 87a4d120 820f4820   **------------------------------ (00000003)  01

Maximum cores per physical processor:   2
Maximum logical processors per core:    1
```

**否**列指示的处理器数。

**PRCB**列指示处理器的处理器控制块的地址。 单独列出每个逻辑处理器。

每个物理处理器有且只有一个逻辑处理器列为**主**下**设置 Master**列。

**SMT 设置**列列出了处理器的同时进行多线程的处理器组信息。

**IAID**列列出了初始高级可编程中断控制器标识符 (APIC ID)。 True x64 计算机上，每个处理器开头是硬编码的初始 APIC id。 可以通过 CPUID 指令检索此 ID 值。 某些其他计算机上初始 APIC ID 却不一定是唯一在所有处理器，因此可通过 APIC 的内存映射的输入/输出 (MMIO) 空间访问 APIC ID 可以在进行修改。 此技术使软件在计算机中的所有处理器分配唯一的 APIC Id。 具体取决于目标计算机的处理器**IAID**列可能会显示此 ID 或可能为空。

 

 





