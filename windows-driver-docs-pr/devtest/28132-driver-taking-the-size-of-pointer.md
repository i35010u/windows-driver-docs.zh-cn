---
title: C28132
description: 警告 C28132 采用指针的大小。
ms.assetid: 9047cfb5-220f-42ad-ba1d-3c1bd43a3423
keywords:
- 警告列出 WDK PREfast for Drivers
- 错误列出 WDK PREfast for Drivers
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28132
ms.openlocfilehash: 7b7834d76fd7a46cda95041ab99cfd7e910db0ae
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63361705"
---
# <a name="c28132"></a>C28132


警告 C28132:获取指针的大小

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>其他信息</strong></p></td>
<td align="left"><p>这将产生的大小 （4 或 8） 的指针，指向不是对象的大小。 取消引用指针，或者如果有意的指针的大小，使用指针类型或 (void *) 相反。</p></td>
</tr>
</tbody>
</table>

 

该驱动程序所花的指针变量，而不是所指向的值的大小的大小。 如果该驱动程序需要指向的值的大小，更改代码，以便它引用的值。 如果该驱动程序实际所需的指针的大小，请与指针类型的大小 (例如，LPSTR， **char\\** * 或甚至 * * void\\* * *) 以阐明，这是意图。

### <a name="span-idexamplespanspan-idexamplespanexample"></a><span id="example"></span><span id="EXAMPLE"></span>示例

下面的代码示例会引起此警告。

```
memset(b, 0, sizeof(b));
```

下面的代码示例可避免此警告。

```
memset(b, 0, sizeof(*b));
```

 

 





