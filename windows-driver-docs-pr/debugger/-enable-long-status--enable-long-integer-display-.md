---
title: .enable_long_status（启用长整数显示）
description: .Enable_long_status 命令指定十进制格式或默认基数，调试器是否显示长整数。
ms.assetid: e08f5a40-5246-4120-ae43-37e876269463
keywords:
- 启用长整数的显示 (.enable_long_status) 命令
- .enable_long_status （启用长整型显示） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .enable_long_status (Enable Long Integer Display)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 2faea3fce198d956ccf0d8652851b925c96b4dce
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336777"
---
# <a name="enablelongstatus-enable-long-integer-display"></a>.enable\_长\_状态 （启用长整数的显示）


**.Enable\_长\_状态**命令指定十进制格式或默认基数，调试器是否显示长整数。

```dbgcmd
.enable_long_status 0 
.enable_long_status 1
```

## <a name="span-idddkmetaenablelongintegerdisplaydbgspanspan-idddkmetaenablelongintegerdisplaydbgspanparameters"></a><span id="ddk_meta_enable_long_integer_display_dbg"></span><span id="DDK_META_ENABLE_LONG_INTEGER_DISPLAY_DBG"></span>参数


<span id="_______0______"></span> **0**   
以十进制格式显示所有的长整数。 这是在调试器的默认行为。

<span id="_______1______"></span> **1**   
显示所有的长整数中的默认基数。

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

**.Enable\_长\_状态**命令影响的输出[ **dt （显示类型）** ](dt--display-type-.md)命令。

在 WinDbg 中， **.enable\_长\_状态**还会影响在显示[局部变量窗口](locals-window.md)和

监视窗口。 这些窗口会自动更新后发出 **.enable\_长\_状态**。

此命令仅影响显示的长整数。 若要控制是否标准中显示整数十进制格式或默认基数，请使用[ **.force\_基数\_输出 （使用基数范围内的整数）** ](-force-radix-output--use-radix-for-integers-.md)命令。

**请注意**   [ **dv （显示本地变量）** ](dv--display-local-variables-.md)命令始终显示在当前的数基的长整数。

 

若要更改默认基数，请使用[ **n (设置数量 Base)** ](n--set-number-base-.md)命令。

 

 





