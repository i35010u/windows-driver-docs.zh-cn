---
title: .force_radix_output（对整数使用基数）
description: .Force_radix_output 命令指定以十进制格式或默认基数中是否显示整数。
ms.assetid: 9ce79919-69fd-426f-8de1-34d0721c35a5
keywords:
- 整数 (.force_radix_output) 命令中使用基数
- .force_radix_output （使用基数范围内的整数） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .force_radix_output (Use Radix for Integers)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 5ca7d5faacd29e0cf8d5c473b56811e02e23a946
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336636"
---
# <a name="forceradixoutput-use-radix-for-integers"></a>.force\_基数\_输出 （使用基数范围内的整数）


**.Force\_基数\_输出**命令指定以十进制格式或默认基数中是否显示整数。

```dbgcmd
.force_radix_output 0 
.force_radix_output 1 
```

## <a name="span-idddkmetauseradixforintegersdbgspanspan-idddkmetauseradixforintegersdbgspanparameters"></a><span id="ddk_meta_use_radix_for_integers_dbg"></span><span id="DDK_META_USE_RADIX_FOR_INTEGERS_DBG"></span>参数


<span id="_______0______"></span> **0**   
以十进制格式显示所有整数 （除外长整型）。 这是在调试器的默认行为。

<span id="_______1______"></span> **1**   
显示默认基数中的所有整数 （除外长整型）。

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

**.Force\_基数\_输出**命令影响的输出[ **dt （显示类型）** ](dt--display-type-.md)命令。

在 WinDbg 中， **.force\_基数\_输出**还会影响在显示[局部变量窗口](locals-window.md)和监视窗口。 可以选择或清除**始终显示在默认数字基数**上的快捷菜单的局部变量或监视窗口将会有相同的效果 **.force\_基数\_输出**。 发出此命令后，会自动更新这些窗口。

**.Force\_基数\_输出**命令仅影响显示内容的标准整数。 若要指定以十进制格式或默认基数显示长整型，使用[ **.enable\_长\_状态 （启用长整数的显示）** ](-enable-long-status--enable-long-integer-display-.md)命令。

若要更改默认基数，请使用[ **n (设置数量 Base)** ](n--set-number-base-.md)命令。

 

 





