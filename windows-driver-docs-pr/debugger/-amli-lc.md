---
title: amli lc
description: Amli lc 扩展会列出所有活动的 ACPI 上下文。
keywords:
- amli lc Windows 调试
ms.date: 09/17/2018
topic_type:
- apiref
api_name:
- amli lc
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 1dc5d802a2cf80d622f0d9a21c863e689420563d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96800067"
---
# <a name="amli-lc"></a>!amli lc


**！ Amli lc** extension 列出所有活动的 ACPI 上下文。

语法

```dbgcmd
   !amli lc
```

## <span id="ddk__amli_lc_dbg"></span><span id="DDK__AMLI_LC_DBG"></span>


### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

Kdexts.dll

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关相关命令及其用法的信息，请参阅 [AMLI 调试器](the-amli-debugger.md)。

<a name="remarks"></a>备注
-------

每个上下文都对应于一个当前在 AML 解释器中运行的方法。

以下是示例：

```console
AMLI(? for help)-> lc
 Ctxt=80e3f000, ThID=00000000, Flgs=A--C-----, pbOp=00000000, Obj=\_SB.LNKA._STA
 Ctxt=80e41000, ThID=00000000, Flgs=A--C-----, pbOp=00000000, Obj=\_SB.LNKB._STA
 Ctxt=80e9a000, ThID=00000000, Flgs=A--C-----, pbOp=00000000, Obj=\_SB.LNKC._STA
 Ctxt=80ea8000, ThID=00000000, Flgs=A--C-----, pbOp=00000000, Obj=\_SB.LNKD._STA
*Ctxt=80e12000, ThID=80e6eda8, Flgs=---CR----, pbOp=80e5d5ac, Obj=\_SB.LNKA._STA
```

**Obj** 字段提供了方法在 ACPI 表中的完整路径和名称。

**Ctxt** 字段提供上下文块的地址。 星号 (**\\** <em>) 指示 * 当前上下文</em>。 这是在发生中断时由解释器执行的上下文。

缩写 **pbOp** 指示指向) 二进制操作代码的指针 (指针。

**Flgs** 节中可显示9个标志。 如果未设置标志，则改为显示连字号。 标志的完整列表如下所示：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">标志</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>A</p></td>
<td align="left"><p>异步计算</p></td>
</tr>
<tr class="even">
<td align="left"><p>N</p></td>
<td align="left"><p>嵌套计算</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Q</p></td>
<td align="left"><p>就绪队列中</p></td>
</tr>
<tr class="even">
<td align="left"><p>C</p></td>
<td align="left"><p>需要回调</p></td>
</tr>
<tr class="odd">
<td align="left"><p>R</p></td>
<td align="left"><p>正在运行</p></td>
</tr>
<tr class="even">
<td align="left"><p>W</p></td>
<td align="left"><p>就绪</p></td>
</tr>
<tr class="odd">
<td align="left"><p>T</p></td>
<td align="left"><p>超时</p></td>
</tr>
<tr class="even">
<td align="left"><p>D</p></td>
<td align="left"><p>计时器调度</p></td>
</tr>
<tr class="odd">
<td align="left"><p>P</p></td>
<td align="left"><p>等待的计时器</p></td>
</tr>
</tbody>
</table>

 

 

 





