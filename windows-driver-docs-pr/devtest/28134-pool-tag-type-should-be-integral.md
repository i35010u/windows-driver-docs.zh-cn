---
title: C28134
description: 警告 C28134 池标记的类型应为整数，而不是字符串或字符串指针。
keywords:
- 列出用于驱动程序的 WDK PREfast 的警告
- 为驱动程序列出的 WDK PREfast 的错误
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28134
ms.openlocfilehash: bf14916c66813cad2341d173bb3de15ff2c53b8b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840407"
---
# <a name="c28134"></a>C28134


警告 C28134：池标记的类型应为整数，而不是字符串或字符串指针

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>其他信息</p></td>
<td align="left"><p>池标记名称应为使用单引号 ( "gaT_" ) 的字符文本，而不是双引号中的字符串。 它通常采用反向字节顺序。</p></td>
</tr>
</tbody>
</table>

 

驱动程序调用一个函数，该函数分配一个池标记（如 [**ExAllocatePoolWithTag**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtag)），但它使用单引号之外的值来指定池标记的值。 不要在池标记中使用带引号的字符串。

### <a name="span-idexamplespanspan-idexamplespanexample"></a><span id="example"></span><span id="EXAMPLE"></span>示例

下面的代码示例 elicits 此警告。

```
p = ExAllocatePoolWithTag(NonPagedPool, 30, "_Tag");
```

下面的代码示例可避免此警告。

```
p = ExAllocatePoolWithTag(NonPagedPool, 30, 'gaT_');
```

 

