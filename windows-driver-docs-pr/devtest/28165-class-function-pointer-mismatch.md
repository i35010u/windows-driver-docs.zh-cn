---
title: C28165
description: 警告 C28165 类的函数指针与函数类不匹配。
ms.assetid: 0fc2b542-058c-4e98-b08e-2661c65e2dd0
keywords:
- 警告列出 WDK PREfast for Drivers
- 错误列出 WDK PREfast for Drivers
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28165
ms.openlocfilehash: dd74ec126a3ac5a3a51c527acbcc34c09fb34558
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564203"
---
# <a name="c28165"></a>C28165


警告 C28165:类的函数指针与函数类不匹配

函数指针具有 **\_ \_drv\_functionClass**指定只有特定的函数类的函数应分配给它的批注。 在分配或隐含的分配中的函数调用中，源和目标必须是同一函数类，但函数类不匹配。

### <a name="span-idexamplespanspan-idexamplespanexample"></a><span id="example"></span><span id="EXAMPLE"></span>示例

下面的代码示例会引起此警告。

```
IoSetCancelRoutine(MyStartIo);
```

下面的代码示例可避免此警告。

```
IoSetCancelRoutine(MyCancelRoutine);
```

 

 





