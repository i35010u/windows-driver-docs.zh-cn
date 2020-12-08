---
title: 期
description: Ate 扩展显示指定地址 (ATE) 的备用页表项。
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
ms.openlocfilehash: e785f79f804f63446a060dbc39cfb964c8925a30
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96800007"
---
# <a name="ate"></a>!ate


**！ Ate** extension 显示指定地址 (ate) 的备用页表项。

```dbgcmd
    !ate Address
```    

**重要提示**  此命令在 Windows 调试器版本10.0.14257 和更高版本中已弃用，不再可用。

 

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span>*地址*   
指定要显示的 ATE。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

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

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关页表和页目录的信息，请参阅 Russinovich 和 David 所罗门群岛的 *Microsoft Windows 内部机制*。 

<a name="remarks"></a>备注
-------

此扩展仅适用于基于 Itanium 的计算机。

下表显示了 ATE 的状态标志。 **！ Ate** 显示表明这些位带有大写字母或短划线并添加了附加信息。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">设置时显示</th>
<th align="left">清除时显示</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>V</p></td>
<td align="left"><p>-</p></td>
<td align="left"><p>立即.</p></td>
</tr>
<tr class="even">
<td align="left"><p>G</p></td>
<td align="left"><p>-</p></td>
<td align="left"><p>未访问。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>E</p></td>
<td align="left"><p>-</p></td>
<td align="left"><p>Execute。</p></td>
</tr>
<tr class="even">
<td align="left"><p>W</p></td>
<td align="left"><p>R</p></td>
<td align="left"><p>可写或只读。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>L</p></td>
<td align="left"><p>-</p></td>
<td align="left"><p>“已锁定”。 ATE 被锁定，因此，在满足当前错误之前，将重试页面上包含 ATE 的任何错误。 在多处理器系统上可能会发生这种情况。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Z</p></td>
<td align="left"><p>-</p></td>
<td align="left"><p>填充零。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>N</p></td>
<td align="left"><p>-</p></td>
<td align="left"><p>无访问权限。</p></td>
</tr>
<tr class="even">
<td align="left"><p>C</p></td>
<td align="left"><p>-</p></td>
<td align="left"><p>写入时复制。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>I</p></td>
<td align="left"><p>-</p></td>
<td align="left"><p>PTE 的间接。 此 ATE 间接引用另一个物理页。 包含 ATE 的页面可能有两个冲突的 ATE 属性。</p></td>
</tr>
<tr class="even">
<td align="left"><p>P</p></td>
<td align="left"></td>
<td align="left"><p>保留。</p></td>
</tr>
</tbody>
</table>

 

 

 





