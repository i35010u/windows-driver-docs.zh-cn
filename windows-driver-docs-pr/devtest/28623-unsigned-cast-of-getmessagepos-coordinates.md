---
title: C28623
description: '警告 C28623 GetMessagePos ( # A1 坐标的未签名强制转换。 使用 GET_X_LPARAM/GET_Y_LPARAM 而不是 LOWORD/HIWORD。'
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28623
ms.openlocfilehash: 4602cd3e7c31669710f79251c99de8218168eb2e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96795635"
---
# <a name="c28623"></a>C28623


警告 C28623： GetMessagePos ( # A1 坐标的未签名强制转换。 使用 GET \_ X \_ LPARAM/get \_ Y \_ LPARAM，而不是 LOWORD/HIWORD

具有多个监视器的系统的 x 坐标和 y 坐标为负。 在此类系统上， **GetMessagePos** 可能会返回负值。 但是，因为 **LOWORD** 和 **HIWORD** 将坐标视为无符号数量，所以不应使用它们。

### <a name="span-idexamplespanspan-idexamplespanexample"></a><span id="example"></span><span id="EXAMPLE"></span>示例

PREfast 报告以下示例的警告。

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

 

 





