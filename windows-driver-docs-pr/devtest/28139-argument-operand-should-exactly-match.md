---
title: C28139
description: 警告 C28139 参数应与类型完全匹配。
keywords:
- 列出用于驱动程序的 WDK PREfast 的警告
- 为驱动程序列出的 WDK PREfast 的错误
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28139
ms.openlocfilehash: d79e8ad352e7b18a9dd14dbb69f1780c4d78df60
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96826137"
---
# <a name="c28139"></a>C28139


警告 C28139：该参数应与类型完全匹配

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>其他信息</p></td>
<td align="left"><p>某些函数允许对参数类型进行有限的算法，而其他函数则不允许。 这通常表示未向枚举正式传递枚举的成员，但也可用于其他类型。</p></td>
</tr>
</tbody>
</table>

 

函数调用中的枚举值与函数声明中为参数指定的类型不匹配。 如果参数错误、缺失或顺序错误，则会出现此错误。 因为 C 允许枚举值互换使用，并可与整数常量互换使用，所以将错误的枚举值传递到函数并不识别错误并不罕见。

如果代码分析工具报告了此错误，请查阅 WDK 中函数的文档。 某些函数编码为仅允许枚举值。 其他一些类型允许 **？：** 运算符在该类型的值之间进行选择，或允许对枚举类型的成员进行算术运算，如将位标志编码为枚举值。 在少数情况下，枚举值和常量可能会组合在一起。

### <a name="span-idexamplespanspan-idexamplespanexample"></a><span id="example"></span><span id="EXAMPLE"></span>示例

下面的代码示例 elicits 此警告。

```
....KeWaitForSingleObject(&MyMutex, UserRequest, UserRequest, false, NULL);
```

下面的代码示例可避免此警告。

```
....KeWaitForSingleObject(&MyMutex, UserRequest, UserMode, false, NULL);
```

 

 





