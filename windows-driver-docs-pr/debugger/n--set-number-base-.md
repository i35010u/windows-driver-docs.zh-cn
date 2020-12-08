---
title: n（设置数字基）
description: N 命令将 (基数) 的默认数字基数设置为指定值或显示当前的基数。请勿将此命令与 ~ n (挂起线程) 命令混淆。
keywords:
- n (设置数字基) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- n (Set Number Base)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: a27a6d1c5ae8694fa99966684cfe24744a27ce83
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96836999"
---
# <a name="n-set-number-base"></a>n（设置数字基）


**N** 命令将 (基数) 的默认数字基数设置为指定值或显示当前的基数。

请勿将此命令与 [**~ n (挂起线程)**](-n--suspend-thread-.md) 命令混淆。

```dbgcmd
n [Radix]
```

## <a name="span-idddk_cmd_set_number_base_dbgspanspan-idddk_cmd_set_number_base_dbgspanparameters"></a><span id="ddk_cmd_set_number_base_dbg"></span><span id="DDK_CMD_SET_NUMBER_BASE_DBG"></span>参数


<span id="_______Radix______"></span><span id="_______radix______"></span><span id="_______RADIX______"></span>*基数*   
指定用于数值显示和输入的默认数字基数。 您可以使用以下值之一。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">“值”</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>8</p></td>
<td align="left"><p>八进制</p></td>
</tr>
<tr class="even">
<td align="left"><p>10</p></td>
<td align="left"><p>小数</p></td>
</tr>
<tr class="odd">
<td align="left"><p>16</p></td>
<td align="left"><p>十六进制</p></td>
</tr>
</tbody>
</table>

 

如果省略了 *基数*，将显示当前的默认数字基数。

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

当前基数影响 MASM 表达式的输入和输出。 它不会影响 c + + 表达式的输入或输出。 有关这些表达式的详细信息，请参阅 [计算表达式](evaluating-expressions.md)。

启动调试器时，默认基数设置为16。

在所有 MASM 表达式中，数字值被解释为当前基数 (16、10或 8) 中的数字。 您可以通过指定 **0x** 前缀 (十六进制) 、 **0n** 前缀 (decimal) 、 **0t** 前缀 (八进制) 或 **w..1 ....** 前缀 (binary) 来覆盖默认基数。

 

 





