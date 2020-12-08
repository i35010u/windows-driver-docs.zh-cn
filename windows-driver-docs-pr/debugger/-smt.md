---
title: smt
description: Smt 扩展显示同时多线程处理器信息的摘要。
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
ms.openlocfilehash: e38feddc1cbcc394864c3cfb484dac9c1eeb1441
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96799843"
---
# <a name="smt"></a>!smt


**！ Smt** 扩展显示同时多线程处理器信息的摘要。

```dbgcmd
!smt
```

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

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

以下是示例：

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

" **否** " 列指示处理器的数量。

**PRCB** 列指示处理器的处理器控制块的地址。 每个逻辑处理器单独列出。

每个物理处理器都只有一个逻辑处理器作为主 **列下的****主服务器** 列出。

**SMT Set** 列列出了处理器的同时多线程处理器集信息。

**IAID** 列列出了初始高级可编程中断控制器标识符 (APIC ID) 。 在真正的 x64 计算机上，每个处理器都以硬编码初始 APIC ID 开头。 可以通过 CPUID 指令检索此 ID 值。 在某些其他计算机上，初始 APIC ID 不一定在所有处理器中是唯一的，因此可以修改通过 APIC 的内存映射输入/输出访问的 APIC ID (MMIO) 空间。 此方法使软件可以为计算机中的所有处理器分配唯一的 APIC Id。 根据目标计算机的处理器， **IAID** 列可能会显示此 ID 或为空。

 

 





