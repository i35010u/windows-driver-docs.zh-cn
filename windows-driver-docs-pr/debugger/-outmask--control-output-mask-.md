---
title: .outmask（控制输出掩码）
description: .Outmask 命令控制当前的输出掩码。
ms.assetid: a925f948-a746-4fed-9ccd-95513f41e3bf
keywords:
- 控制输出掩码 (.outmask) 命令
- .outmask （控制输出掩码） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .outmask (Control Output Mask)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 953176c909b580c2d04b0305c1d690755a6c453f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334427"
---
# <a name="outmask-control-output-mask"></a>.outmask（控制输出掩码）


**.Outmask**命令控制当前的输出掩码。

```dbgcmd
.outmask[-] [/l] Expression 
.outmask /a 
.outmask /d
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______Expression______"></span><span id="_______expression______"></span><span id="_______EXPRESSION______"></span> *表达式*   
指定要添加到掩码的标志。 *表达式*可以是任何 ULONG 值，该值指定所需的标志位。 有关可能的标志列表，请参阅备注部分中的表。

<span id="_______-______"></span> **-**   
移除 bits，*表达式*指定的掩码，而不是将它们添加到掩码中。

<span id="________l______"></span><span id="________L______"></span> **/l**   
将保留日志文件的输出掩码的当前值。 如果不包括 **/l**，日志文件的输出掩码是常规输出掩码相同。

<span id="________a______"></span><span id="________A______"></span> **/a**   
激活所有掩码标志。 此参数等效于 **.outmask 0xFFFFFFFF**。

<span id="________d______"></span><span id="________D______"></span> **/d**   
将输出掩码还原为默认值。 此参数等效于 **.outmask 0x3F7**。

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

每个输出掩码标志可使调试器能够显示在某些输出[调试器命令窗口](debugger-command-window.md)。 如果所有的掩码标志被设置，将显示所有输出。

应删除输出掩码标志小心，因为您可能无法读取调试器输出。

下面的标志值存在。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ReplTest1</th>
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
<td align="left"><p>关闭</p></td>
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
<td align="left"><p>注册之前提示转储</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x40</p></td>
<td align="left"><p>开</p></td>
<td align="left"><p>特定于扩展操作的警告</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x80</p></td>
<td align="left"><p>开</p></td>
<td align="left"><p>调试目标输出 (例如， <strong>OutputDebugString</strong>或<strong>DbgPrint</strong>)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x100</p></td>
<td align="left"><p>开</p></td>
<td align="left"><p>调试目标所需的输入 (例如， <strong>DbgPrompt</strong>)</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x200</p></td>
<td align="left"><p>开</p></td>
<td align="left"><p>符号的消息 (例如， <strong>！ 符号干扰</strong>)</p></td>
</tr>
</tbody>
</table>

 

 

 





