---
title: .force_radix_output（对整数使用基数）
description: .Force_radix_output 命令指定是以十进制格式还是在默认基数中显示整数。
keywords:
- 为整数 ( .force_radix_output) 命令使用基数
- .force_radix_output (对 Windows 调试) 整数使用基数
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .force_radix_output (Use Radix for Integers)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: e3775c9103d2752db5970d65de170c08217e0f52
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96822651"
---
# <a name="force_radix_output-use-radix-for-integers"></a>。 \_ \_ (对整数使用基数，则强制使用基数输出) 


**Force \_ 基数 \_ output** 命令指定是以十进制格式还是在默认基数中显示整数。

```dbgcmd
.force_radix_output 0 
.force_radix_output 1 
```

## <a name="span-idddk_meta_use_radix_for_integers_dbgspanspan-idddk_meta_use_radix_for_integers_dbgspanparameters"></a><span id="ddk_meta_use_radix_for_integers_dbg"></span><span id="DDK_META_USE_RADIX_FOR_INTEGERS_DBG"></span>参数


<span id="_______0______"></span>**0**   
显示除十进制格式) 的长整数以外的所有整数 (。 这是调试器的默认行为。

<span id="_______1______"></span>**1**   
显示默认基数) 除长整数以外的所有整数 (。

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

**Force \_ 基数 \_ output** 命令会影响 [**dt (显示类型)**](dt--display-type-.md)命令的输出。

在 WinDbg 中，" **强制 \_ 基数 \_ 输出** " 还会影响 " [局部变量" 窗口](locals-window.md) 和 "监视窗口" 中的显示。 可以在 "局部变量" 或 "监视窗口" 的快捷菜单上选择或清除 " **始终在默认基数中显示数字** "，使其效果与 " **强制 \_ 基数 \_ 输出**" 相同。 发出此命令后，这些窗口会自动更新。

**Force \_ 基数 \_ output** 命令只影响标准整数的显示。 若要指定是以十进制格式还是按默认基数显示长整数，请使用 [**。启用 \_ 长 \_ 状态 (启用长整数显示)**](-enable-long-status--enable-long-integer-display-.md) 命令。

若要更改默认基数，请使用 [**n (设置 Number Base)**](n--set-number-base-.md) 命令。

 

 





