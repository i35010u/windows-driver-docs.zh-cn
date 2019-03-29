---
title: .excr（显示异常上下文记录）
description: .Excr 命令将显示与当前异常相关联的上下文记录。
ms.assetid: 18FD32B9-93DE-4E23-A73C-18CC3665417A
keywords:
- .excr （显示异常上下文记录） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .excr (Display Exception Context Record)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: fe946b014e9e28735868082b7318246d9aaa92b4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567624"
---
# <a name="excr-display-exception-context-record"></a>.excr（显示异常上下文记录）


**.Excr**命令将显示与当前异常相关联的上下文记录。

```dbgcmd
.excr
```

## <span id="ddk_meta_display_exception_context_record_dbg"></span><span id="DDK_META_DISPLAY_EXCEPTION_CONTEXT_RECORD_DBG"></span>


### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>模式</strong></p></td>
<td align="left"><p>仅限用户模式</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>仅用于故障转储 （仅适用于小型转储）</p></td>
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

**.Excr**命令查找当前异常的上下文信息，并显示指定的上下文记录的重要寄存器。

此命令也指示调试器使用与当前寄存器上下文作为异常相关联的上下文记录。 运行后 **.excr**，调试器可以访问最重要的寄存器和堆栈跟踪此线程。 启用目标以执行、 更改当前进程或线程，或使用另一个寄存器上下文命令之前将一直保留此寄存器上下文 ([**.cxr** ](-cxr--display-context-record-.md)或 **.excr**). 有关注册上下文的详细信息，请参阅[注册上下文](changing-contexts.md#register-context)。

[ **.Ecxr** ](-ecxr--display-exception-context-record-.md)命令是同义词命令，并具有相同的功能。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**.ecxr**](-ecxr--display-exception-context-record-.md)

 

 






