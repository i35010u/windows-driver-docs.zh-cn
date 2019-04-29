---
title: uf（取消汇编函数）
description: 如果命令显示指定函数的程序集转换在内存中。
ms.assetid: 344e3afd-6b8d-48f2-9e07-dd7e1937f71b
keywords:
- 如果 （反汇编函数） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- uf (Unassemble Function)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 5e4dd50771339718b2a6c77a6c062100db3e8dca
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380769"
---
# <a name="uf-unassemble-function"></a>uf（取消汇编函数）


**Uf**命令显示指定函数的程序集转换在内存中。

```dbgcmd
uf [Options] Address
```

## <a name="span-idddkcmdunassemblefunctiondbgspanspan-idddkcmdunassemblefunctiondbgspanparameters"></a><span id="ddk_cmd_unassemble_function_dbg"></span><span id="DDK_CMD_UNASSEMBLE_FUNCTION_DBG"></span>参数


<span id="_______Options______"></span><span id="_______options______"></span><span id="_______OPTIONS______"></span> *选项*   
一个或多个以下选项：

<span id="_c"></span><span id="_C"></span>**/c**  
显示仅调用指令，而不是完整的反汇编的例程中。 调用指令可用于确定从反汇编代码的调用方和被调用方关系。

<span id="_D"></span><span id="_d"></span>**/D**  
创建用于导航的调用关系图的链接被调用方名称。

<span id="_m"></span><span id="_M"></span>**/m**  
解除阻止的要求，以允许多个退出。

<span id="_o"></span><span id="_O"></span>**/o**  
对显示的地址，而不是由函数偏移量进行排序。 此选项提供了完整的函数的内存布局视图。

<span id="_O"></span><span id="_o"></span>**/O**  
为访问调用的信息和创建断点，请创建链接的调用行。

<span id="_i"></span><span id="_I"></span>**/i**  
例程中显示指令的数。

<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *Address*   
指定要拆装的函数的地址。 有关语法的详细信息，请参阅[地址和地址范围语法](address-and-address-range-syntax.md)。

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

屏幕将显示整个函数中，根据函数顺序。

 

 





