---
title: uf（取消汇编函数）
description: Uf 命令显示内存中指定函数的程序集转换。
keywords:
- ) Windows 调试的 uf (Unassemble 函数
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- uf (Unassemble Function)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 205906282ab913ebe6d0c90d0086a7ff01116013
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803253"
---
# <a name="uf-unassemble-function"></a>uf（取消汇编函数）


**Uf** 命令显示内存中指定函数的程序集转换。

```dbgcmd
uf [Options] Address
```

## <a name="span-idddk_cmd_unassemble_function_dbgspanspan-idddk_cmd_unassemble_function_dbgspanparameters"></a><span id="ddk_cmd_unassemble_function_dbg"></span><span id="DDK_CMD_UNASSEMBLE_FUNCTION_DBG"></span>参数


<span id="_______Options______"></span><span id="_______options______"></span><span id="_______OPTIONS______"></span>*选项*   
以下一个或多个选项：

<span id="_c"></span><span id="_C"></span>**/c**  
只显示例程中的调用说明，而不是完整的反汇编。 调用指令可用于从反汇编代码确定调用方和被调用方的关系。

<span id="_D"></span><span id="_d"></span>**/D**  
创建链接的被调用方名称以导航调用关系图。

<span id="_m"></span><span id="_M"></span>**一样**  
放宽阻止要求，以允许多个退出。

<span id="_o"></span><span id="_O"></span>**/o**  
按地址而不是函数偏移量对显示进行排序。 此选项显示完整函数的内存布局视图。

<span id="_O"></span><span id="_o"></span>**/O**  
创建用于访问调用信息和创建断点的链接调用线。

<span id="_i"></span><span id="_I"></span>**/i**  
显示例程中的指令数。

<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span>*地址*   
指定要反汇编的函数的地址。 有关语法的详细信息，请参阅 [address 和 Address Range 语法](address-and-address-range-syntax.md)。

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

显示将根据函数顺序显示整个函数。

 

 





