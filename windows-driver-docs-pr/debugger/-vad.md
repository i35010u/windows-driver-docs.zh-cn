---
title: vad
description: Vad 扩展显示的虚拟地址说明符 (VAD) 的详细信息或 Vad 树。
ms.assetid: 96bd5a38-016d-4ce9-b128-cc730577be45
keywords:
- 虚拟地址说明符 (VAD)
- VAD （虚拟地址描述符）
- 地址，虚拟地址说明符 (VAD)
- vad Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- vad
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b79e0b54bc1134b84cf3d1b9402861e668836a71
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63323491"
---
# <a name="vad"></a>!vad


**！ Vad**扩展显示的虚拟地址说明符 (VAD) 的详细信息或 Vad 树。

-   显示一个虚拟地址说明符 (VAD) 的详细信息
-   显示 Vad 树的详细信息。
-   显示有关特定的用户模式模块 Vad 信息并提供可用于加载该模块的符号的字符串。

```dbgcmd
!vad VAD-Root [Flag]
!vad Address 1
```

## <a name="span-idddkvaddbgspanspan-idddkvaddbgspanparameters"></a><span id="ddk__vad_dbg"></span><span id="DDK__VAD_DBG"></span>参数


<span id="_______VAD-Root______"></span><span id="_______vad-root______"></span><span id="_______VAD-ROOT______"></span> *VAD-Root*   
要显示的 VAD 树的根的地址。

<span id="_______Flag______"></span><span id="_______flag______"></span><span id="_______FLAG______"></span> *Flag*   
指定在窗体显示。 可能值的包括：

<span id="0"></span>0  
在基于整个 VAD 树*VAD 根*显示。 （这是默认值）。

<span id="1"></span>1  
通过指定 VAD *VAD 根*显示。 显示将包含更详细的分析。

<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *Address*   
在用户模式模块的虚拟地址范围中的地址。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

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

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关虚拟地址描述符信息，请参阅*Microsoft Windows Internals*、 Mark Russinovich 和 David solomon 合著的。 

<a name="remarks"></a>备注
-------

可以使用找到的地址的任何进程 VAD 根目录[ **！ 过程**](-process.md)命令。

**！ Vad**命令时需要加载已分页内存不足的用户模式模块的符号可以提供帮助。 有关详细信息，请参阅[映射符号时 PEB 是分页出](mapping-symbols-when-the-peb-is-paged-out.md)。

下面是举例 **！ vad**扩展：

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

 

 





