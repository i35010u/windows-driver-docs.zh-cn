---
title: 导入内核模式安全整数函数
description: 内核模式安全整数函数作为内联代码提供，该代码包含在 ntintsafe 或您将代码链接到的库中。
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 3f2d6f1f8b503f7c6f133ce700bba4cf1d25d1a8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96788649"
---
# <a name="importing-kernel-mode-safe-integer-functions"></a>导入内核模式安全整数函数


内核模式安全整数函数作为内联代码提供，该代码包含在 ntintsafe 或您将代码链接到的库中。 此标头文件在 Windows 驱动程序工具包 (WDK) 中可用。

请注意，必须对无符号值使用算术运算，这一点很重要。 若要使用带符号的值，必须先使用转换函数将有符号值安全地转换为无符号值，然后再使用算术函数。

## <a name="to-use-the-inline-versions-of-the-kernel-mode-safe-integer-functions"></a>使用内核模式安全整数函数的内联版本


包括头文件，如下所示。

```ManagedCPlusPlus
#include <ntintsafe.h>
```

 

 




