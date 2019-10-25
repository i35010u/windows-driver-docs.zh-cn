---
title: C28134
description: 警告 C28134 池标记的类型应为整数，而不是字符串或字符串指针。
ms.assetid: f61aec4c-4072-421f-aa6d-d9399d0c439c
keywords:
- 列出用于驱动程序的 WDK PREfast 的警告
- 为驱动程序列出的 WDK PREfast 的错误
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28134
ms.openlocfilehash: c266c44ad2ca609f53fe8203a454fbf9682243cc
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840317"
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
<td align="left"><p><strong>附加信息</strong></p></td>
<td align="left"><p>池标记名称应为使用单引号（' gaT_ '）的字符文本，而不能是双引号中的字符串。 它通常采用反向字节顺序。</p></td>
</tr>
</tbody>
</table>

 

驱动程序调用一个函数，该函数分配一个池标记（如[**ExAllocatePoolWithTag**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtag)），但它使用单引号之外的值来指定池标记的值。 不要在池标记中使用带引号的字符串。

### <a name="span-idexamplespanspan-idexamplespanexample"></a><span id="example"></span><span id="EXAMPLE"></span>实例

下面的代码示例 elicits 此警告。

```
p = ExAllocatePoolWithTag(NonPagedPool, 30, "_Tag");
```

下面的代码示例可避免此警告。

```
p = ExAllocatePoolWithTag(NonPagedPool, 30, 'gaT_');
```

 

 





