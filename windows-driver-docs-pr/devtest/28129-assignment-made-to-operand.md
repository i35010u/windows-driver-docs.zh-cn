---
title: C28129
description: 警告的 C28129 操作数，仅应使用位设置和清除修改对进行了赋值。
ms.assetid: b5afad45-6498-42f3-b1aa-9ba3cc8abb6d
keywords:
- 警告列出 WDK PREfast for Drivers
- 错误列出 WDK PREfast for Drivers
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28129
ms.openlocfilehash: d62f0973b5f806675ea1a428d0b4388ec4a7e250
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63361406"
---
# <a name="c28129"></a>C28129


警告 C28129:分配对操作数，应仅修改使用位设置和清除

该驱动程序正在使用赋值修改操作数。 分配一个值可能无意中更改的值的位数而非其需要改变，从而导致意外的结果。

### <a name="span-idexamplespanspan-idexamplespanexample"></a><span id="example"></span><span id="EXAMPLE"></span>示例

下面的代码示例会引起此警告。

```
fdo->Flags = DO_BUFFERED_IO;
```

下面的代码示例可避免此警告。

```
fdo->Flags |= DO_BUFFERED_IO;
```

 

 





