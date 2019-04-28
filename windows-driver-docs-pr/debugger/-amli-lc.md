---
title: amli lc
description: Amli lc 扩展列出所有活动的 ACPI 上下文。
ms.assetid: 070db570-ab8c-47ce-88fa-dc5f16c1c2ee
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
ms.openlocfilehash: ff147399d03ba9688024a7a6468e09ccb3937741
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63337023"
---
# <a name="amli-lc"></a>!amli lc


**！ Amli lc**扩展列出所有活动的 ACPI 上下文。

语法

```dbgcmd
   !amli lc
```

## <span id="ddk__amli_lc_dbg"></span><span id="DDK__AMLI_LC_DBG"></span>


### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Kdexts.dll

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关相关的命令及其用途的信息，请参阅[AMLI 调试器](the-amli-debugger.md)。

<a name="remarks"></a>备注
-------

每个上下文对应于当前在 AML 解释器中运行的方法。

下面是一个示例：

```console
AMLI(? for help)-> lc
 Ctxt=80e3f000, ThID=00000000, Flgs=A--C-----, pbOp=00000000, Obj=\_SB.LNKA._STA
 Ctxt=80e41000, ThID=00000000, Flgs=A--C-----, pbOp=00000000, Obj=\_SB.LNKB._STA
 Ctxt=80e9a000, ThID=00000000, Flgs=A--C-----, pbOp=00000000, Obj=\_SB.LNKC._STA
 Ctxt=80ea8000, ThID=00000000, Flgs=A--C-----, pbOp=00000000, Obj=\_SB.LNKD._STA
*Ctxt=80e12000, ThID=80e6eda8, Flgs=---CR----, pbOp=80e5d5ac, Obj=\_SB.LNKA._STA
```

**Obj**字段提供的完整路径和方法的名称显示在 ACPI 表中。

**Ctxt**字段提供上下文块的地址。 星号 (**\\**<em>) 指示 * 当前上下文</em>。 这是已由解释器在中断发生时执行的上下文。

缩写**pbOp**指示指令指针 （指向二进制操作代码）。

有可中显示的九个标志**Flgs**部分。 如果未设置一个标志，改为显示以连字符。 标志的完整列表如下所示：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Flag</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>A</p></td>
<td align="left"><p>异步评估</p></td>
</tr>
<tr class="even">
<td align="left"><p>N</p></td>
<td align="left"><p>嵌套的评估</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Q</p></td>
<td align="left"><p>在准备就绪的队列</p></td>
</tr>
<tr class="even">
<td align="left"><p>C</p></td>
<td align="left"><p>需要一个回调</p></td>
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
<td align="left"><p>挂起的计时器</p></td>
</tr>
</tbody>
</table>

 

 

 





