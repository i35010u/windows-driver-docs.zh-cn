---
title: C28139
description: 警告 C28139 参数应与类型完全匹配。
ms.assetid: c20b39c2-eee7-4265-ac2f-39023da16549
keywords:
- 警告列出 WDK PREfast for Drivers
- 错误列出 WDK PREfast for Drivers
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28139
ms.openlocfilehash: d5173df1bf4b9c5e2b62b0d976a67582f48b2270
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63361389"
---
# <a name="c28139"></a>C28139


警告 C28139:参数应与类型完全匹配

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>其他信息</strong></p></td>
<td align="left"><p>某些函数的自变量类型上允许有限的算术运算，其他人不这样做。 这通常表示为枚举形式未传递的枚举成员，但不能用于其他类型。</p></td>
</tr>
</tbody>
</table>

 

函数调用中的枚举的值与函数声明中的参数指定的类型不匹配。 编码错误、 缺少的或无序参数时会出现此错误。 因为 C 允许枚举互换，并与整数常量互换使用的值，它不是将错误的枚举的值传递给函数，而无需识别该错误不常见。

如果代码分析工具将报告此错误，请参阅 WDK 中函数的文档。 某些函数被编码以便允许仅枚举的值。 其他允许 **？:** 要选择该类型的值之间或允许对枚举的类型，如当位标志被编码为一个枚举值的成员进行算术运算符。 在少数情况下，可能会组合枚举的值和常量。

### <a name="span-idexamplespanspan-idexamplespanexample"></a><span id="example"></span><span id="EXAMPLE"></span>示例

下面的代码示例会引起此警告。

```
....KeWaitForSingleObject(&MyMutex, UserRequest, UserRequest, false, NULL);
```

下面的代码示例可避免此警告。

```
....KeWaitForSingleObject(&MyMutex, UserRequest, UserMode, false, NULL);
```

 

 





