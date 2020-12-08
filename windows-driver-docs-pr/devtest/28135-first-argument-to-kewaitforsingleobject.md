---
title: C28135
description: 警告 C28135 如果 KeWaitForSingleObject 的第一个参数是本地变量，则 Mode 参数必须为 KernelMode。
keywords:
- 列出用于驱动程序的 WDK PREfast 的警告
- 为驱动程序列出的 WDK PREfast 的错误
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28135
ms.openlocfilehash: 8d1f0f40e1404b70b67e331aaf3c642d0ffaf8d9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840405"
---
# <a name="c28135"></a>C28135


警告 C28135：如果 KeWaitForSingleObject 的第一个参数是本地变量，则 Mode 参数必须为 KernelMode

驱动程序正在用户模式下等待。 因此，可以在等待期间换出内核堆栈。 如果驱动程序尝试在堆栈上传递参数，则可能会导致系统崩溃。

### <a name="span-idexamplespanspan-idexamplespanexample"></a><span id="example"></span><span id="EXAMPLE"></span>示例

下面的代码示例 elicits 此警告。

```
KeWaitForSingleObject(&MyMutex, UserRequest, UserMode, false, NULL);
```

下面的代码示例可避免此警告。

```
KeWaitForSingleObject(&MyMutex, UserRequest, KernelMode, false, NULL);
```

 

 





