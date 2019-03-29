---
title: C28714
description: 语义不同的整数类型之间的警告 C28714 强制转换。
ms.assetid: 53acc1a1-58a9-4009-a15c-2b11f31b086d
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28714
ms.openlocfilehash: 977ae0125efd1a82f872367ed5335311b477ac62
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577418"
---
# <a name="c28714"></a>C28714


警告 C28714:语义不同的整数类型之间强制转换

此警告意味着**NTSTATUS**值要显式强制转换为 Boolean 类型。 这很可能产生意外结果。 例如，典型的成功值**NTSTATUS**，**状态\_成功**，为**false**时作为一个布尔值进行测试。

在大多数情况下， **NT\_成功**宏应该用于测试的值**NTSTATUS**。 此宏将返回 **，则返回 true**如果返回的状态值为一条警告和错误代码都不。 如果某个函数返回一个布尔值，以指示其失败/成功，它应显式返回相应的布尔类型而不是依赖于的强制转换**NTSTATUS**为 Boolean 类型。

此外，有时程序可能会尝试重复使用一个布尔值的本地变量来存储**NTSTATUS**值。 这种做法通常是容易出错;它会更安全 (和可能效率更高) 使用单独**NTSTATUS**变量。

 

 





