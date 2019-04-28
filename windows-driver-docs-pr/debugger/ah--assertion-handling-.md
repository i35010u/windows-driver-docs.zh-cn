---
title: ah（断言处理）
description: Ah 命令控制处理为特定地址的状态的断言。
ms.assetid: a55aa34f-c861-45de-bacf-92549ab98fdc
keywords:
- ah （断言处理） 的 Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ah (Assertion Handling)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 36ef3af780fb85093d8ad257543b8975c8e5800c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63355019"
---
# <a name="ah-assertion-handling"></a>ah（断言处理）


**Ah**命令控制处理为特定地址的状态的断言。

```dbgcmd
ahb [Address] 
ahi [Address] 
ahd [Address] 
ahc 
ah 
```

## <a name="span-idddkcmdassertionhandlingdbgspanspan-idddkcmdassertionhandlingdbgspanparameters"></a><span id="ddk_cmd_assertion_handling_dbg"></span><span id="DDK_CMD_ASSERTION_HANDLING_DBG"></span>参数


<span id="_______ahb______"></span><span id="_______AHB______"></span> **ahb**   
如果在指定的地址失败断言，进入调试器。

<span id="_______ahi"></span><span id="_______AHI"></span> **ahi**  
将忽略在指定地址断言失败。

<span id="_______ahd______"></span><span id="_______AHD______"></span> **ahd**   
删除指定地址处的任何断言处理信息。 此删除操作会导致调试器以返回到其默认状态，以便该地址。

<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *Address*   
指定要设置其断言处理状态的指令的地址。 如果省略此参数，则调试器将使用当前的程序计数器。

<span id="_______ahc"></span><span id="_______AHC"></span> **ahc**  
删除当前进程的所有断言处理信息。

<span id="_______ah______"></span><span id="_______AH______"></span> **ah**   
显示当前的断言处理设置。

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
<td align="left"><p>仅实时调试</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关中断状态和处理状态、 所有事件代码的说明、 所有事件和控制此状态的其他方法的详细信息的默认状态的列表的详细信息，请参阅[控制异常和事件](controlling-exceptions-and-events.md).

<a name="remarks"></a>备注
-------

**Ah\\*** 命令控制处理特定地址的状态的断言。 [ **Sx\* asrt** ](sx--sxd--sxe--sxi--sxn--sxr--sx---set-exceptions-.md)命令控制处理状态的全局断言。 如果您使用**ah\\*** 调试器为某个地址，然后声明发生那里，响应根据**ah\\*** 设置，并忽略**sx\* asrt**设置。

当调试器遇到断言时，调试器首先会检查是否已为该特定地址配置处理。 如果还没有配置处理，调试器将使用的全局设置。

**Ah\\*** 命令仅影响当前进程。 当前进程结束时，状态的所有设置都都将丢失。

断言处理状态才会影响仅有状态\_断言\_异常的异常。 这种空格处理不会影响的内核模式断言例程。

 

 





