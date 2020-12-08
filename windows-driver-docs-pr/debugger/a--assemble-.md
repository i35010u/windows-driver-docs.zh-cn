---
title: a（汇编）
description: A 命令汇编32位 x86 指令助记键，并将生成的指令代码放入内存。
keywords:
- 组合 () 命令
- 程序集调试，汇编 () 命令
- " (汇编) Windows 调试"
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- a (Assemble)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 69372565965597e9a1d5d27a3948b70db9bd84cb
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96819333"
---
# <a name="a-assemble"></a>a（汇编）


**A** 命令汇编32位 x86 指令助记键，并将生成的指令代码放入内存。

```dbgcmd
a [Address]
```

## <a name="span-idddk_cmd_assemble_dbgspanparameters"></a><span id="DDK_CMD_ASSEMBLE_DBG"></span>参数


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span>*地址*   
指定放置生成代码的内存块的开头。 有关语法的详细信息，请参阅 [address 和 Address Range 语法](address-and-address-range-syntax.md)。

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

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关程序集调试和相关命令的详细信息，请参阅 [程序集模式下的调试](debugging-in-assembly-mode.md)。

<a name="remarks"></a>备注
-------

**A** 命令不支持64位指令助记键。 但是，无论是调试32位目标还是64位目标，都将启用 **a** 命令。 由于 x86 和 x64 指令之间的相似之处，因此在调试64位目标时，有时可以成功使用 **a** 命令。

如果不指定地址，程序集将从指令指针的当前值指定的地址开始。 若要组合新指令，请键入所需的助记键，然后按 ENTER。 若要结束程序集，请按 ENTER。

由于汇编程序会搜索代码中引用的所有符号，因此此命令可能需要一段时间才能完成。 在此期间，不能按 [**CTRL + C**](ctrl-c--break-.md)结束 **某个** 命令。

 

 





