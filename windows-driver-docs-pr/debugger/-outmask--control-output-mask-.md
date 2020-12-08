---
title: .outmask（控制输出掩码）
description: Outmask 命令控制当前输出掩码。
keywords:
- " () 命令控制输出掩码"
- outmask (控件输出掩码) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .outmask (Control Output Mask)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 8902ec03b1aa3b51f2620d0f4a7d77488f3eef1b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96811259"
---
# <a name="outmask-control-output-mask"></a>.outmask（控制输出掩码）


**Outmask** 命令控制当前输出掩码。

```dbgcmd
.outmask[-] [/l] Expression 
.outmask /a 
.outmask /d
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______Expression______"></span><span id="_______expression______"></span><span id="_______EXPRESSION______"></span>*表达式*   
指定要添加到掩码的标志。 *Expression* 可以是指定所需标志位的任何 ULONG 值。 有关可能的标志的列表，请参阅 "备注" 部分中的表。

<span id="_______-______"></span> **-**   
从掩码中删除 *Expression* 指定的位，而不是将其添加到掩码。

<span id="________l______"></span><span id="________L______"></span>**/l**   
保留日志文件的输出掩码的当前值。 如果不包括 **/l**，则日志文件的输出掩码与常规输出掩码相同。

<span id="________a______"></span><span id="________A______"></span>**/a**   
激活所有掩码标志。 此参数等效于 **. Outmask 0xffffffff**。

<span id="________d______"></span><span id="________D______"></span>**/d**   
将输出掩码还原为默认值。 此参数等效于 **. Outmask 0x3F7**。

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
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

每个输出掩码标志都允许调试器在 [调试器命令窗口](debugger-command-window.md)中显示特定的输出。 如果设置了所有掩码标志，则显示所有输出。

你应小心删除输出掩码标志，因为你可能无法读取调试器输出。

存在下列标志值。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">“值”</th>
<th align="left">默认设置</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>1</p></td>
<td align="left"><p>开</p></td>
<td align="left"><p>正常输出</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>开</p></td>
<td align="left"><p>错误输出</p></td>
</tr>
<tr class="odd">
<td align="left"><p>4</p></td>
<td align="left"><p>开</p></td>
<td align="left"><p>警告</p></td>
</tr>
<tr class="even">
<td align="left"><p>8</p></td>
<td align="left"><p>关</p></td>
<td align="left"><p>其他输出</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x10</p></td>
<td align="left"><p>开</p></td>
<td align="left"><p>提示输出</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x20</p></td>
<td align="left"><p>开</p></td>
<td align="left"><p>提示前注册转储</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x40</p></td>
<td align="left"><p>开</p></td>
<td align="left"><p>特定于扩展操作的警告</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x80</p></td>
<td align="left"><p>开</p></td>
<td align="left"><p>从目标 (调试输出例如， <strong>OutputDebugString</strong> 或 <strong>DbgPrint</strong>) </p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x100</p></td>
<td align="left"><p>开</p></td>
<td align="left"><p>调试目标 (所需的输入，例如， <strong>DbgPrompt</strong>) </p></td>
</tr>
<tr class="even">
<td align="left"><p>0x200</p></td>
<td align="left"><p>开</p></td>
<td align="left"><p>符号消息 (例如， <strong>！符号干扰</strong>) </p></td>
</tr>
</tbody>
</table>

 

 

 





