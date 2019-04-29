---
title: C28134
description: 警告 C28134 池标记的类型应为整型、 不字符串或字符串的指针。
ms.assetid: f61aec4c-4072-421f-aa6d-d9399d0c439c
keywords:
- 警告列出 WDK PREfast for Drivers
- 错误列出 WDK PREfast for Drivers
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28134
ms.openlocfilehash: 373e85d31a3ca2bc9d90974523d0d2d9abbb2c39
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63361409"
---
# <a name="c28134"></a>C28134


警告 C28134:池标记的类型应整型，而不是字符串或字符串指针

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>其他信息</strong></p></td>
<td align="left"><p>池标记名称应为字符文本使用单引号 ('gaT_) 不是在双引号内的字符串。 它通常是以反向字节顺序。</p></td>
</tr>
</tbody>
</table>

 

该驱动程序正在调用的函数分配的池标记，如[ **ExAllocatePoolWithTag**](https://msdn.microsoft.com/library/windows/hardware/ff544520)，但它用单引号引起来使用文本以外的值，指定池标记的值。 不要在池标记中使用带引号的字符串。

### <a name="span-idexamplespanspan-idexamplespanexample"></a><span id="example"></span><span id="EXAMPLE"></span>示例

下面的代码示例会引起此警告。

```
p = ExAllocatePoolWithTag(NonPagedPool, 30, "_Tag");
```

下面的代码示例可避免此警告。

```
p = ExAllocatePoolWithTag(NonPagedPool, 30, 'gaT_');
```

 

 





