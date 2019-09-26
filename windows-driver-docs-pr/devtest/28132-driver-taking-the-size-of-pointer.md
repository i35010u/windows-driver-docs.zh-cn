---
title: C28132
description: 警告 C28132 采用指针大小。
ms.assetid: 9047cfb5-220f-42ad-ba1d-3c1bd43a3423
keywords:
- 列出用于驱动程序的 WDK PREfast 的警告
- 为驱动程序列出的 WDK PREfast 的错误
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28132
ms.openlocfilehash: 19d604687fe6cced382f764d3da73827dc6c6b5e
ms.sourcegitcommit: 9dbb1ef59c3e797bfc3cc418dd2b9bdc44940d14
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/26/2019
ms.locfileid: "71284983"
---
# <a name="c28132"></a>C28132


警告 C28132：获取指针的大小

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>附加信息</strong></p></td>
<td align="left"><p>这将产生指针的大小（4或8），而不是指向的对象的大小。 取消引用指针，或者如果要使用指针的大小，请改用指针类型或（void *）。</p></td>
</tr>
</tbody>
</table>

 

驱动程序使用指针变量的大小，而不是指向的值的大小。 如果驱动程序需要指向值的大小，请更改代码，使其引用该值。 如果驱动程序确实需要指针的大小，请使用指针类型的大小（例如，LPSTR、 **char\*** 甚至是**void\*** ）来阐明这是目的。

### <a name="span-idexamplespanspan-idexamplespanexample"></a><span id="example"></span><span id="EXAMPLE"></span>实例

下面的代码示例 elicits 此警告。

```
memset(b, 0, sizeof(b));
```

下面的代码示例可避免此警告。

```
memset(b, 0, sizeof(*b));
```

 

 





