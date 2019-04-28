---
title: .cxr（显示上下文记录）
description: .Cxr 命令显示指定地址处保存的上下文记录。 它还设置寄存器上下文。
ms.assetid: 0e882639-6029-4512-8d46-050228e95cb6
keywords:
- 显示上下文记录 (.cxr) 命令
- 上下文记录
- .cxr （显示上下文记录） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .cxr (Display Context Record)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 6fcedc429b537dea85194ce04ef331fa576d7d62
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336878"
---
# <a name="cxr-display-context-record"></a>.cxr（显示上下文记录）


**.Cxr**命令显示指定地址处保存的上下文记录。 它还设置寄存器上下文。

```dbgsyntax
.cxr [Options] [Address]  
```

## <a name="span-idddkmetadisplaycontextrecorddbgspanspan-idddkmetadisplaycontextrecorddbgspanparameters"></a><span id="ddk_meta_display_context_record_dbg"></span><span id="DDK_META_DISPLAY_CONTEXT_RECORD_DBG"></span>参数


<span id="_______Options______"></span><span id="_______options______"></span><span id="_______OPTIONS______"></span> *选项*   
可以是下列选项中的任意组合：

<span id="_f_Size"></span><span id="_f_size"></span><span id="_F_SIZE"></span>**/f** **** *大小*  
上下文大小等于的值将强制*大小*，以字节为单位。 上下文不匹配时的实际目标-例如，使用 x86 时这很有用期间的 64 位目标的上下文*WOW64*调试。 如果指定了无效或不一致的大小，则将显示错误消息"无法转换为规范格式的上下文"。

<span id="_w"></span><span id="_W"></span>**/w**  
当前上下文写入内存，并显示已写入的位置的地址。

<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *Address*   
系统上下文记录的地址。

省略地址不显示任何上下文记录信息，但它重置原理寄存器上下文。

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

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关寄存器上下文和其他上下文设置的详细信息，请参阅[更改上下文](changing-contexts.md)。

<a name="remarks"></a>备注
-------

从上下文记录的信息可以用于帮助调试系统停止其中发生了未经处理的异常和确切的堆栈跟踪不可用。 **.Cxr**命令显示指定的上下文记录的重要寄存器。

此命令还指示调试器使用指定的上下文记录作为寄存器上下文。 执行此命令后，调试器将具有访问此线程的最重要的寄存器和堆栈跟踪。 允许目标以执行或使用另一个寄存器上下文命令之前将一直保留此寄存器上下文 ([**.thread**](-thread--set-register-context-.md)， [ **.ecxr** ](-ecxr--display-exception-context-record-.md)， [ **.trap** ](-trap--display-trap-frame-.md) ，或 **.cxr**再次)。 在用户模式下，它还将会重置更改当前进程或线程。 请参阅[注册上下文](changing-contexts.md#register-context)有关详细信息。

**.Cxr**命令通常用于调试 bug 检查 0x1E。 有关详细信息和示例，请参阅[ **Bug 检查 0x1E** ](bug-check-0x1e--kmode-exception-not-handled.md) (KMODE\_异常\_不\_HANDLED)。

**.Cxr /w**命令上下文写入内存，并显示存储的位置的地址。 此地址可以传递给[ **.apply\_dbp （到上下文应用数据断点）** ](-apply-dbp--apply-data-breakpoint-to-context-.md)如果需要应用到此上下文的数据断点。

 

 





