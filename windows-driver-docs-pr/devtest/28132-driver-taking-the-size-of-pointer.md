---
title: C28132
description: 警告 C28132 采用指针大小。
keywords:
- 列出用于驱动程序的 WDK PREfast 的警告
- 为驱动程序列出的 WDK PREfast 的错误
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28132
ms.openlocfilehash: 4994b059c56e332365f94431aeef37e32a4c4069
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840409"
---
# <a name="c28132"></a>C28132


警告 C28132：采用指针的大小

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>其他信息</p></td>
<td align="left"><p>这将产生指针 (4 或 8) 的大小，而不是指向的对象的大小。 取消引用指针，或者如果要使用指针的大小，请改用指针类型或 (void * ) 。</p></td>
</tr>
</tbody>
</table>

 

驱动程序使用指针变量的大小，而不是指向的值的大小。 如果驱动程序需要指向值的大小，请更改代码，使其引用该值。 如果驱动程序确实需要指针的大小，请采用指针类型的大小 (例如，LPSTR、**char \** _ 甚至是 _*void \**_) 来阐明这是目的。

### <a name="span-idexamplespanspan-idexamplespanexample"></a><span id="example"></span><span id="EXAMPLE"></span>示例

下面的代码示例 elicits 此警告。

```
memset(b, 0, sizeof(b));
```

下面的代码示例可避免此警告。

```
memset(b, 0, sizeof(_b));
```

 

 





