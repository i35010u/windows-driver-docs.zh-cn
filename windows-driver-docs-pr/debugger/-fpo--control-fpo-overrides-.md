---
title: .fpo（控制 FPO 替代）
description: .Fpo 命令控制帧指针省略 (FPO) 替代。
ms.assetid: a1a20f5d-71c9-487b-bcba-a87b60d74588
keywords:
- .fpo （重写控件 FPO） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .fpo (Control FPO Overrides)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 4f5d395cc83473a7003830004e506d23e5f757ca
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336614"
---
# <a name="fpo-control-fpo-overrides"></a>.fpo（控制 FPO 替代）


**.Fpo**命令控制帧指针省略 (FPO) 替代。

```dbgcmd
.fpo -s [-fFlag] Address 
.fpo -d Address 
.fpo -x Address 
.fpo -o Address 
.fpo Address 
```

## <a name="span-idddk_meta_control_fpo_overrides_dbgspanspan-idddk_meta_control_fpo_overrides_dbgspanparameters"></a><span id="ddk_meta_control_fpo_overrides_dbg"></span><span id="DDK_META_CONTROL_FPO_OVERRIDES_DBG"></span>参数


<span id="_______-s______"></span><span id="_______-S______"></span> **-s**   
指定地址处设置 FPO 重写。

<span id="_______-fFlag______"></span><span id="_______-fflag______"></span><span id="_______-FFLAG______"></span> * *-f***Flag*   
指定用于重写 FPO 标志。 绝对不能添加之间有空格 **-f**并*标志*。 如果该标志会采用一个参数，则必须添加标志和该参数之间有空格。 如果你希望多个标志，则必须重复 **-f**切换 (例如， **-fb-fp 4-fe**)。 可以使用 **-f**开关仅与 **-s**。 可以使用以下值之一*标志*。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Flag</th>
<th align="left">效果</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>b</strong></p></td>
<td align="left"><p>集<strong>fUseBP</strong>等于<strong>TRUE</strong>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>e</strong></p></td>
<td align="left"><p>集<strong>fUseSEH</strong>等于<strong>TRUE</strong>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>n</strong></p></td>
<td align="left"><p>集<strong>cbFrame</strong>等于 FRAME_NONFPO。 （默认情况下，cbFrame 设置为 FRAME_FPO。）</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>l</strong>  <em>Term</em></p></td>
<td align="left"><p>集<strong>cdwLocals</strong>等于<em>术语</em>。 <em>术语</em>应指定所需的本地 DWORD 计数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>p</strong>  <em>Term</em></p></td>
<td align="left"><p>集<strong>cdwParams</strong>等于<em>术语</em>。 <em>术语</em>应指定参数所需的双字节计数。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>r</strong>  <em>Term</em></p></td>
<td align="left"><p>集<strong>cbRegs</strong>等于<em>术语</em>。 <em>术语</em>应指定所需的注册计数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>s</strong>   <em>术语</em></p></td>
<td align="left"><p>集<strong>cbProcSize</strong>等于<em>术语</em>。 <em>术语</em>应指定所需的过程大小。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>t</strong>  <em>Term</em></p></td>
<td align="left"><p>集<strong>cbFrame</strong>等于<em>术语</em>。 <em>术语</em>应指定下面的帧类型之一：</p>
<ul>
<li><p>FRAME_FPO 0</p></li>
<li><p>FRAME_TRAP 1</p></li>
<li><p>FRAME_TSS 2</p></li>
<li><p>FRAME_NONFPO 3</p></li>
</ul></td>
</tr>
</tbody>
</table>

 

<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *Address*   
指定调试器设置或删除重写或调试器应显示其替代的地址的位置的地址。 该地址必须是当前模块列表中的模块中。

<span id="_______-d______"></span><span id="_______-D______"></span> -**d**   
删除指定地址处的 FPO 重写。

<span id="_______-x______"></span><span id="_______-X______"></span> **-x**   
删除包含的模块中的所有 FPO 替代*地址*地址。

<span id="_______-o______"></span><span id="_______-O______"></span> **-o**   
显示包含的模块中的所有 FPO 替代*地址*地址。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>模式</strong></p></td>
<td align="left"><p>用户模式下，内核模式</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>实时、 崩溃转储</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

不带参数， **.fpo**命令显示指定的地址的 FPO 重写。

一些编译器 （包括 Microsoft Visual Studio 6.0 及更早版本） 生成 FPO 信息以指示如何设置堆栈帧。 在堆栈遍历，调试器使用这些 FPO 记录了解堆栈。 如果编译器生成 FPO 信息不正确，则可以使用 **.fpo**命令以修复此问题。

 

 





