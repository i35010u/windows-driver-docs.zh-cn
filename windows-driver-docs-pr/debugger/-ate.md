---
title: ate
description: Ate 扩展显示指定的地址的备用页表项 (ATE)。
ms.assetid: 8ec98fa5-4939-49cb-8678-e412b9cbe7e3
keywords:
- ate Windows 调试
ms.date: 09/17/2018
topic_type:
- apiref
api_name:
- ate
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 7ab77539705532e390a987c867ed591444b7ac5c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334725"
---
# <a name="ate"></a>!ate


**！ Ate**扩展显示指定的地址的备用页表项 (ATE)。

```dbgcmd
    !ate Address
```    

**重要**  此命令已被 Windows 调试器版本 10.0.14257 中不推荐使用和更高版本，并不再可用。

 

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *Address*   
指定要显示 ATE。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>不可用</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 及更高版本</strong></p></td>
<td align="left"><p>Kdexts.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关页表和页目录中的信息，请参阅*Microsoft Windows Internals*、 Mark Russinovich 和 David solomon 合著的。 

<a name="remarks"></a>备注
-------

此扩展才可在基于 Itanium 的计算机上。

下表中显示 ATE 的状态标志。 **！ Ate**显示指示这些位与大写字母或短划线和添加其他信息。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">显示时设置</th>
<th align="left">显示时清除</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>V</p></td>
<td align="left"><p>-</p></td>
<td align="left"><p>提交。</p></td>
</tr>
<tr class="even">
<td align="left"><p>G</p></td>
<td align="left"><p>-</p></td>
<td align="left"><p>不能访问。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>E</p></td>
<td align="left"><p>-</p></td>
<td align="left"><p>执行。</p></td>
</tr>
<tr class="even">
<td align="left"><p>W</p></td>
<td align="left"><p>R</p></td>
<td align="left"><p>可写或只读的。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>L</p></td>
<td align="left"><p>-</p></td>
<td align="left"><p>“已锁定”。 ATE 处于锁定状态，因此，包含 ATE 任何错误的页上将重试，直到满足当前的错误。 这可以在多处理器系统上。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Z</p></td>
<td align="left"><p>-</p></td>
<td align="left"><p>填充零。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>N</p></td>
<td align="left"><p>-</p></td>
<td align="left"><p>没有访问权限。</p></td>
</tr>
<tr class="even">
<td align="left"><p>C</p></td>
<td align="left"><p>-</p></td>
<td align="left"><p>将复制中写入。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>I</p></td>
<td align="left"><p>-</p></td>
<td align="left"><p>PTE 间接。 此 ATE 间接引用另一个物理页。 包含 ATE 的页可能具有两个冲突 ATE 属性。</p></td>
</tr>
<tr class="even">
<td align="left"><p>P</p></td>
<td align="left"></td>
<td align="left"><p>保留。</p></td>
</tr>
</tbody>
</table>

 

 

 





