---
title: vad
description: Vad 扩展显示虚拟地址描述符 (VAD) 或 Vad 树的详细信息。
keywords:
- '虚拟地址描述符 (VAD) '
- 'VAD (虚拟地址描述符) '
- '地址，虚拟地址描述符 (VAD) '
- vad Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- vad
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 4b1723c8474f78d720c260d3fbaa57c4565b8188
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96833848"
---
# <a name="vad"></a>!vad


**！ Vad** 扩展显示虚拟地址描述符 (vad) 或 vad 树的详细信息。

-   显示 (VAD 的一个虚拟地址描述符的详细信息) 
-   显示 Vad 的树的详细信息。
-   显示有关特定用户模式模块的 Vad 的信息，并提供可用于加载该模块的符号的字符串。

```dbgcmd
!vad VAD-Root [Flag]
!vad Address 1
```

## <a name="span-idddk__vad_dbgspanspan-idddk__vad_dbgspanparameters"></a><span id="ddk__vad_dbg"></span><span id="DDK__VAD_DBG"></span>参数


<span id="_______VAD-Root______"></span><span id="_______vad-root______"></span><span id="_______VAD-ROOT______"></span>*VAD-根*   
要显示的 VAD 树的根地址。

<span id="_______Flag______"></span><span id="_______flag______"></span><span id="_______FLAG______"></span>*标志*   
指定显示的窗体。 可能的值包括：

<span id="0"></span>0  
此时将显示基于 *VAD* 的整个 VAD 树。  (这是默认值。 ) 

<span id="1"></span>1  
仅显示由 *VAD* 指定的 VAD。 显示将包括更详细的分析。

<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span>*地址*   
用户模式模块的虚拟地址范围内的地址。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Windows 2000</p></td>
<td align="left"><p>Kdextx86.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p>Windows XP 及更高版本</p></td>
<td align="left"><p>Kdexts.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关虚拟地址描述符的详细信息，请参阅 Russinovich 和 David 所罗门群岛上的 *Microsoft Windows 内部机制*。 

<a name="remarks"></a>备注
-------

使用 [**！ process**](-process.md) 命令可找到任何进程的 VAD 的根地址。

当你需要为已分页出内存的用户模式模块加载符号时， **！ vad** 命令会很有帮助。 有关详细信息，请参阅 [在 PEB 被分页时映射符号](mapping-symbols-when-the-peb-is-paged-out.md)。

下面是 **！ vad** 扩展的一个示例：

```dbgcmd
kd> !vad 824bc2f8
VAD     level      start      end    commit
82741bf8 ( 1)      78000    78045         8 Mapped  Exe  EXECUTE_WRITECOPY
824ef368 ( 2)      7f6f0    7f7ef         0 Mapped       EXECUTE_READ
824bc2f8 ( 0)      7ffb0    7ffd3         0 Mapped       READONLY
8273e508 ( 2)      7ffde    7ffde         1 Private      EXECUTE_READWRITE
82643fc8 ( 1)      7ffdf    7ffdf         1 Private      EXECUTE_READWRITE

Total VADs:     5  average level:    2  maximum depth: 2

kd> !vad 824bc2f8 1

VAD @ 824bc2f8
  Start VPN:         7ffb0  End VPN:    7ffd3  Control Area:  827f1208
  First ProtoPte: e1008500  Last PTE e100858c  Commit Charge         0 (0.)
  Secured.Flink          0  Blink           0  Banked/Extend:        0 Offset 0
   ViewShare NoChange READONLY

SecNoChange 
```

 

 





