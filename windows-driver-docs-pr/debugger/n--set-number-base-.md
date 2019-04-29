---
title: n（设置数字基）
description: N 个命令将默认数基 （基数） 设置为指定值，或显示基本的当前数目。不要混淆此命令使用 ~ n （挂起线程） 命令。
ms.assetid: a2af7cf4-b0f1-4ceb-b9c0-7517a9517c3e
keywords:
- n （集基础货币） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- n (Set Number Base)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 3c2c1e5e9c10adff45a1d86c6aaf55a69096676a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380495"
---
# <a name="n-set-number-base"></a>n（设置数字基）


**N**命令将默认数基 （基数） 设置为指定值或显示基本的当前数目。

不要将使用此命令相混淆[ **~ （挂起线程） n** ](-n--suspend-thread-.md)命令。

```dbgcmd
n [Radix]
```

## <a name="span-idddkcmdsetnumberbasedbgspanspan-idddkcmdsetnumberbasedbgspanparameters"></a><span id="ddk_cmd_set_number_base_dbg"></span><span id="DDK_CMD_SET_NUMBER_BASE_DBG"></span>参数


<span id="_______Radix______"></span><span id="_______radix______"></span><span id="_______RADIX______"></span> *Radix*   
指定的默认数目基用于数字显示和条目。 可以使用以下值之一。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">值</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>8</p></td>
<td align="left"><p>八进制</p></td>
</tr>
<tr class="even">
<td align="left"><p>10</p></td>
<td align="left"><p>Decimal</p></td>
</tr>
<tr class="odd">
<td align="left"><p>16</p></td>
<td align="left"><p>十六进制</p></td>
</tr>
</tbody>
</table>

 

如果省略*基数*，显示当前的默认数基。

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

输入和输出的 MASM 表达式会影响当前的基数。 它不影响的输入或输出的C++表达式。 有关这些表达式的详细信息，请参阅[评估表达式](evaluating-expressions.md)。

启动调试器时，默认基数设置为 16。

在所有 MASM 表达式中，数字值被解释为当前基数 （16、 10 或 8） 中的数字。 可以通过指定重写默认基数**0x**前缀 （十六进制） **0n**前缀 （十进制） **0t**前缀 （八进制） 或**0y**前缀 （二进制）。

 

 





