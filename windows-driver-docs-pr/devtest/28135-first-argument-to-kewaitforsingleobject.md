---
title: C28135
description: 警告 C28135 如果 KeWaitForSingleObject 的第一个参数是一个本地变量，则 Mode 参数必须为 KernelMode。
ms.assetid: f42e41d7-240f-4de1-97b7-e50415aee14f
keywords:
- 警告列出 WDK PREfast for Drivers
- 错误列出 WDK PREfast for Drivers
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28135
ms.openlocfilehash: 5ca20bf7553f43b6e8dfca9e5822c54ef45d65e1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63361399"
---
# <a name="c28135"></a>C28135


警告 C28135:如果 KeWaitForSingleObject 的第一个参数是本地变量，则 Mode 参数必须为 KernelMode

该驱动程序正在等待在用户模式下。 在这种情况下，内核堆栈可以在等待期间换出中。 如果驱动程序将尝试将参数传递到堆栈上，可能会导致系统崩溃。

### <a name="span-idexamplespanspan-idexamplespanexample"></a><span id="example"></span><span id="EXAMPLE"></span>示例

下面的代码示例会引起此警告。

```
KeWaitForSingleObject(&MyMutex, UserRequest, UserMode, false, NULL);
```

下面的代码示例可避免此警告。

```
KeWaitForSingleObject(&MyMutex, UserRequest, KernelMode, false, NULL);
```

 

 





