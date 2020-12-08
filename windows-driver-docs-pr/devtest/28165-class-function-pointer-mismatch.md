---
title: C28165
description: 警告 C28165 类的函数指针与函数类不匹配。
keywords:
- 列出用于驱动程序的 WDK PREfast 的警告
- 为驱动程序列出的 WDK PREfast 的错误
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28165
ms.openlocfilehash: 6714262aa42bf52f281a77491a2f3ea7725ffca0
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96793137"
---
# <a name="c28165"></a>C28165


警告 C28165：类的函数指针与函数类不匹配

函数指针具有 **\_ \_ winspool.drv \_ functionClass** 批注，该批注指定仅应为特定功能类分配函数。 在函数调用的分配或隐含分配中，源和目标必须是同一函数类，但函数类不匹配。

### <a name="span-idexamplespanspan-idexamplespanexample"></a><span id="example"></span><span id="EXAMPLE"></span>示例

下面的代码示例 elicits 此警告。

```
IoSetCancelRoutine(MyStartIo);
```

下面的代码示例可避免此警告。

```
IoSetCancelRoutine(MyCancelRoutine);
```

 

 





