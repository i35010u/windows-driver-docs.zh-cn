---
title: .cxr（显示上下文记录）
description: .Cxr 命令显示保存在指定地址的上下文记录。 它还设置注册上下文。
keywords:
- " ( 中显示上下文记录) 命令"
- 上下文记录
- .cxr (显示) Windows 调试的上下文记录
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .cxr (Display Context Record)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: eaa6b79b592d7d2239698f704e35530c860c9ef3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803323"
---
# <a name="cxr-display-context-record"></a>.cxr（显示上下文记录）


**.Cxr** 命令显示保存在指定地址的上下文记录。 它还设置注册上下文。

```dbgsyntax
.cxr [Options] [Address]  
```

## <a name="span-idddk_meta_display_context_record_dbgspanspan-idddk_meta_display_context_record_dbgspanparameters"></a><span id="ddk_meta_display_context_record_dbg"></span><span id="DDK_META_DISPLAY_CONTEXT_RECORD_DBG"></span>参数


<span id="_______Options______"></span><span id="_______options______"></span><span id="_______OPTIONS______"></span>*选项*   
可以是下列选项的任意组合：

<span id="_f_Size"></span><span id="_f_size"></span><span id="_F_SIZE"></span>**/f**  **** *大小*  
强制上下文大小等于 *大小* 的值（以字节为单位）。 当上下文与实际目标不匹配时，这可能很有用，例如，当在 *WOW64* 调试期间在64位目标上使用 x86 上下文时，这会很有用。 如果指定的大小无效或不一致，将显示错误 "无法将上下文转换为规范格式"。

<span id="_w"></span><span id="_W"></span>**/w**  
将当前上下文写入内存，并显示写入该上下文的位置的地址。

<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span>*地址*   
系统上下文记录的地址。

省略地址不会显示任何上下文记录信息，但会重置注册上下文。

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
<td align="left"><p>all</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关注册上下文和其他上下文设置的详细信息，请参阅 [更改上下文](changing-contexts.md)。

<a name="remarks"></a>备注
-------

上下文记录中的信息可用于帮助调试系统暂停，其中发生了未处理的异常，并且准确的堆栈跟踪不可用。 **.Cxr** 命令显示指定上下文记录的重要寄存器。

此命令还指示调试器使用指定的上下文记录作为寄存器上下文。 执行此命令后，调试器将有权访问此线程的最重要寄存器和堆栈跟踪。 此注册上下文会一直 [**保留，直到**](-trap--display-trap-frame-.md)你允许目标执行或使用另一个寄存器上下文 [**命令 () 。**](-thread--set-register-context-.md) [**.ecxr**](-ecxr--display-exception-context-record-.md) **.cxr** 在用户模式下，如果您更改当前进程或线程，还会重置。 有关详细信息，请参阅 [注册上下文](changing-contexts.md#register-context) 。

**.Cxr** 命令通常用于调试 Bug 检查0x1E。 有关详细信息和示例，请参阅 [**Bug 检查 0x1E**](bug-check-0x1e--kmode-exception-not-handled.md) (\_ \_ 未 \_ 处理的 KMODE 异常) 。

**.Cxr/w** 命令将上下文写入内存，并显示存储它的地址。 此地址可传递给。如果需要将数据断点应用到此上下文，请 [**\_ (将数据断点应用于上下文) 。**](-apply-dbp--apply-data-breakpoint-to-context-.md)

 

 





