---
title: .fpo（控制 FPO 替代）
description: Fpo 命令控制框架指针省略 (FPO) 重写。
keywords:
- " (控制 FPO 重写) Windows 调试"
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .fpo (Control FPO Overrides)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 2377406b44f8cf8c293a11057a4acaf81b754c05
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96824395"
---
# <a name="fpo-control-fpo-overrides"></a>.fpo（控制 FPO 替代）


**Fpo** 命令控制框架指针省略 (fpo) 重写。

```dbgcmd
.fpo -s [-fFlag] Address 
.fpo -d Address 
.fpo -x Address 
.fpo -o Address 
.fpo Address 
```

## <a name="span-idddk_meta_control_fpo_overrides_dbgspanspan-idddk_meta_control_fpo_overrides_dbgspanparameters"></a><span id="ddk_meta_control_fpo_overrides_dbg"></span><span id="DDK_META_CONTROL_FPO_OVERRIDES_DBG"></span>参数


<span id="_______-s______"></span><span id="_______-S______"></span>**-s**   
设置指定地址处的 FPO 重写。

<span id="_______-fFlag______"></span><span id="_______-fflag______"></span><span id="_______-FFLAG______"></span>**-f**_标志_   
指定替代的 FPO 标志。 不能在 **-f** 和 *标志* 之间添加空格。 如果标志采用参数，则必须在标志和该参数之间添加一个空格。 如果需要多个标志，则必须重复 **-f** 开关 (例如， **-fb-fp 4-fe**) 。 只能将 **-f** 开关与 **-s** 一起使用。 您可以使用以下值之一作为 *标志*。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">标志</th>
<th align="left">效果</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>b</strong></p></td>
<td align="left"><p>将 <strong>fUseBP</strong> 设置为 <strong>TRUE</strong>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>e</strong></p></td>
<td align="left"><p>将 <strong>fUseSEH</strong> 设置为 <strong>TRUE</strong>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>n</strong></p></td>
<td align="left"><p>将 <strong>cbFrame</strong> 设置为等于 FRAME_NONFPO。  (默认情况下，cbFrame 设置为 FRAME_FPO。 ) </p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>l</strong> <strong></strong> <em>术语</em></p></td>
<td align="left"><p>设置 <strong>cdwLocals</strong> 等于 <em>Term</em>。 <em>字词</em> 应指定所需的本地 DWORD 计数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>p</strong> <strong></strong> <em>项</em></p></td>
<td align="left"><p>设置 <strong>cdwParams</strong> 等于 <em>Term</em>。 <em>字词</em> 应指定所需的参数 DWORD 计数。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>r</strong> <strong></strong> <em>术语</em></p></td>
<td align="left"><p>设置 <strong>cbRegs</strong> 等于 <em>Term</em>。 <em>字词</em> 应指定所需的寄存器计数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>s</strong> <strong></strong> <em>术语</em></p></td>
<td align="left"><p>设置 <strong>cbProcSize</strong> 等于 <em>Term</em>。 <em>字词</em> 应指定所需的过程大小。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>t</strong> <strong></strong> <em>术语</em></p></td>
<td align="left"><p>设置 <strong>cbFrame</strong> 等于 <em>Term</em>。 <em>字词</em> 应指定以下帧类型之一：</p>
<ul>
<li><p>FRAME_FPO 0</p></li>
<li><p>FRAME_TRAP 1</p></li>
<li><p>FRAME_TSS 2</p></li>
<li><p>FRAME_NONFPO 3</p></li>
</ul></td>
</tr>
</tbody>
</table>

 

<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span>*地址*   
指定调试器在其中设置或删除重写的地址或其替代调试器应显示的地址。 此地址必须在当前模块列表的模块中。

<span id="_______-d______"></span><span id="_______-D______"></span> -**2-d**   
删除指定地址处的 FPO 重写。

<span id="_______-x______"></span><span id="_______-X______"></span>**-x**   
删除包含 *地址* 地址的模块内的所有 FPO 重写。

<span id="_______-o______"></span><span id="_______-O______"></span>**-o**   
显示包含 *地址* 地址的模块内的所有 FPO 重写。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>交货</strong></p></td>
<td align="left"><p>用户模式，内核模式</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>实时，故障转储</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>all</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

如果没有参数，则 **. fpo** 命令显示指定地址的 fpo 重写。

一些编译器 (包括 Microsoft Visual Studio 6.0 及更早版本) 生成 FPO 信息以指示堆栈帧的设置方式。 在堆栈遍历期间，调试器使用这些 FPO 记录来理解堆栈。 如果编译器生成了错误的 FPO 信息，你可以使用 **FPO** 命令来解决此问题。

 

 





