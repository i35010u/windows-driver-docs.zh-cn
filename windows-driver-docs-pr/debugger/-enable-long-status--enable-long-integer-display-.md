---
title: .enable_long_status（启用长整数显示）
description: .Enable_long_status 命令指定调试器是以十进制格式还是按默认基数显示长整数。
keywords:
- 启用 ( .enable_long_status) 命令的长整数显示
- .enable_long_status (在 Windows 调试) 启用长整数显示
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .enable_long_status (Enable Long Integer Display)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 907da3b5bb17ab260e9bd2c0ea2f216de5550b89
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96811289"
---
# <a name="enable_long_status-enable-long-integer-display"></a>。启用 \_ 长时间 \_ 状态 (启用长整数显示) 


**. 启用 \_ 长 \_ 状态** 命令指定调试器是以十进制格式还是在默认基数中显示长整数。

```dbgcmd
.enable_long_status 0 
.enable_long_status 1
```

## <a name="span-idddk_meta_enable_long_integer_display_dbgspanspan-idddk_meta_enable_long_integer_display_dbgspanparameters"></a><span id="ddk_meta_enable_long_integer_display_dbg"></span><span id="DDK_META_ENABLE_LONG_INTEGER_DISPLAY_DBG"></span>参数


<span id="_______0______"></span>**0**   
以十进制格式显示所有长整数。 这是调试器的默认行为。

<span id="_______1______"></span>**1**   
显示默认基数中的所有长整数。

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

**. 启用 \_ 长 \_ 状态** 命令会影响 [**dt (显示类型)**](dt--display-type-.md)命令的输出。

在 WinDbg 中， **启用 " \_ 长" \_ 状态** 还会影响 " [局部变量" 窗口](locals-window.md) 中的显示和

监视窗口。 发出后，这些窗口会自动更新 **。启用 " \_ 长" \_ 状态**。

此命令仅影响长整数的显示。 若要控制标准整数是以十进制格式还是按默认基数显示，请使用 [**. force \_ 基数 \_ 输出 (对整数使用基数)**](-force-radix-output--use-radix-for-integers-.md) 命令。

**注意**  [**Dv (显示局部变量)**](dv--display-local-variables-.md) 命令始终在当前数字基数中显示长整数。

 

若要更改默认基数，请使用 [**n (设置 Number Base)**](n--set-number-base-.md) 命令。

 

 





