---
title: ah（断言处理）
description: Ah 命令控制特定地址的断言处理状态。
keywords:
- ah (断言处理) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ah (Assertion Handling)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 57ec7eec2b47d336ef1e31cc1206bd11ea6d04fe
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96808515"
---
# <a name="ah-assertion-handling"></a>ah（断言处理）


**Ah** 命令控制特定地址的断言处理状态。

```dbgcmd
ahb [Address] 
ahi [Address] 
ahd [Address] 
ahc 
ah 
```

## <a name="span-idddk_cmd_assertion_handling_dbgspanspan-idddk_cmd_assertion_handling_dbgspanparameters"></a><span id="ddk_cmd_assertion_handling_dbg"></span><span id="DDK_CMD_ASSERTION_HANDLING_DBG"></span>参数


<span id="_______ahb______"></span><span id="_______AHB______"></span>**ahb**   
如果指定地址处的断言失败，则中断调试器。

<span id="_______ahi"></span><span id="_______AHI"></span>**ahi**  
忽略指定地址处的断言失败。

<span id="_______ahd______"></span><span id="_______AHD______"></span>**ahd**   
删除指定地址处的任何断言处理信息。 此删除操作会使调试器返回到该地址的默认状态。

<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span>*地址*   
指定正在设置其断言处理状态的指令的地址。 如果省略此参数，则调试器将使用当前程序计数器。

<span id="_______ahc"></span><span id="_______AHC"></span>**ahc**  
删除当前进程的所有断言处理信息。

<span id="_______ah______"></span><span id="_______AH______"></span>**ah**   
显示当前断言处理设置。

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
<td align="left"><p>仅限实时调试</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关中断状态和处理状态、所有事件代码的说明、所有事件的默认状态的列表以及有关控制此状态的其他方法的详细信息，请参阅 [控制异常和事件](controlling-exceptions-and-events.md)。

<a name="remarks"></a>备注
-------

**Ah \\** _ 命令控制特定地址的断言处理状态。 [_ *Sx \* asrt* *](sx--sxd--sxe--sxi--sxn--sxr--sx---set-exceptions-.md)命令控制全局断言处理状态。 如果对某个地址使用 **ah \\** _，然后在其中进行断言，则调试器将根据 _*ah \\* *_ 设置进行响应，并忽略 _ *sx \* asrt** 设置。

当调试器遇到断言时，调试器首先检查是否为该特定地址配置了处理。 如果尚未配置处理，则调试器将使用全局设置。

**Ah \\*** 命令仅影响当前进程。 当前进程结束时，所有状态设置都将丢失。

断言处理状态仅影响状态 \_ 断言 \_ 异常异常。 此处理不会影响内核模式断言例程。

 

 





