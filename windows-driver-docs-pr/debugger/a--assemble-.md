---
title: a（汇编）
description: 命令对 32 位 x86 指令助记键和放到内存中生成的指令代码。
ms.assetid: 6736a5fd-5a33-4698-9510-8a95f6a1caf7
keywords:
- 组合 (a) 命令
- 调试时，程序集组合 (a) 命令
- （汇编） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- a (Assemble)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f77510936fbc6d3073b300b1ccd52a4cf5c531e3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63351495"
---
# <a name="a-assemble"></a>a（汇编）


的命令对 32 位 x86 指令助记键和放到内存中生成的指令代码。

```dbgcmd
a [Address]
```

## <a name="span-idddkcmdassembledbgspanparameters"></a><span id="DDK_CMD_ASSEMBLE_DBG"></span>参数


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *Address*   
指定在其中放置生成代码的内存块的开头。 有关语法的详细信息，请参阅[地址和地址范围语法](address-and-address-range-syntax.md)。

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

调试和相关命令，请参阅有关程序集的详细信息[在程序集模式下调试](debugging-in-assembly-mode.md)。

<a name="remarks"></a>备注
-------

命令不支持 64 位指令助记键。 但是， 命令启用而不考虑在调试 32 位目标或 64 位目标。 由于 x86 和 x64 说明之间的相似之处，有时可以使用命令成功调试 64 位目标时。

如果不指定一个地址，该程序集开始于指令指针的当前值指定的地址。 组装新指令，键入所需的助记键，然后按 ENTER。 若要结束的程序集，请按仅 ENTER。

在组装器中搜索的所有代码中引用的符号，因为此命令可能需要时间才能完成。 在此期间，不能按[ **CTRL + C**](ctrl-c--break-.md)结束命令。

 

 





