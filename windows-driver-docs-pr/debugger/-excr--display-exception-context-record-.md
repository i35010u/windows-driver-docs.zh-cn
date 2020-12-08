---
title: .excr（显示异常上下文记录）
description: Excr 命令显示与当前异常关联的上下文记录。
keywords:
- excr (显示) Windows 调试的异常上下文记录
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .excr (Display Exception Context Record)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 7f68248bb4647007f4d48d3fd09876cc608b5748
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96805861"
---
# <a name="excr-display-exception-context-record"></a>.excr（显示异常上下文记录）


**Excr** 命令显示与当前异常关联的上下文记录。

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
<td align="left"><p><strong>交货</strong></p></td>
<td align="left"><p>仅用户模式</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>故障转储仅 (小型转储仅) </p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关注册上下文和其他上下文设置的详细信息，请参阅 [更改上下文](changing-contexts.md)。

<a name="remarks"></a>备注
-------

**Excr** 命令查找当前异常的上下文信息，并显示指定上下文记录的重要寄存器。

此命令还指示调试器使用与当前异常关联的上下文记录作为注册上下文。 运行 **excr** 后，调试器可以访问此线程最重要的寄存器和堆栈跟踪。 此注册上下文会一直保留，直到你启用目标执行、更改当前进程或线程，或使用另一个注册上下文命令 ([**.cxr**](-cxr--display-context-record-.md) 或 **excr**) 。 有关注册上下文的详细信息，请参阅 [注册上下文](changing-contexts.md#register-context)。

[**Ecxr**](-ecxr--display-exception-context-record-.md)命令是一个同义词命令，它具有相同的功能。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**.ecxr**](-ecxr--display-exception-context-record-.md)

 

 






