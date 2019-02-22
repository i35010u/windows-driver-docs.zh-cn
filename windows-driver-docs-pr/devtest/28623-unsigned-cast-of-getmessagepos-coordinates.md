---
title: C28623
description: 警告 GetMessagePos() 坐标 C28623 无符号强制转换。 使用 GET_X_LPARAM/GET_Y_LPARAM，而不是使用 LOWORD/HIWORD。
ms.assetid: 155da4f5-4e77-451e-b26b-69a39c32effa
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28623
ms.openlocfilehash: bb3c2190439e84f27557a4cdea2353ab5bcb7400
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542473"
---
# <a name="c28623"></a>C28623


警告 C28623:无符号强制转换 GetMessagePos() 坐标。 使用 GET\_X\_LPARAM/GET\_Y\_LPARAM 而不是使用 LOWORD/HIWORD

具有多个监视器的系统可以具有负的 x 坐标和 y 坐标。 在此类系统中， **GetMessagePos**可能因此返回负值。 但是，由于**使用 LOWORD**并**HIWORD**坐标视为无符号的数量，它们不应使用。

### <a name="span-idexamplespanspan-idexamplespanexample"></a><span id="example"></span><span id="EXAMPLE"></span>示例

PREfast 报告的警告的下面的示例。

```
DWORD dw = GetMessagePos();
POINT ppt;

ppt.x = LOWORD(dw);
ppt.y = HIWORD(dw);
```

下面的示例可避免此错误。

```
DWORD dw = GetMessagePos();
POINT ppt;

ppt.x = GET_X_LPARAM(dw);
ppt.y = GET_Y_LPARAM(dw);
```

 

 





