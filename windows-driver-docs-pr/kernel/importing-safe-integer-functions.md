---
title: 导入内核模式安全整数函数
description: 内核模式安全整数函数都可用作在 ntintsafe.h 或链接到代码库中包含的内联代码。
ms.assetid: C6696C4E-952A-4162-B2BE-F262496FFBD2
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: ecb667fc5ffd86f52c62eb1db13ec8f21c9558cc
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555413"
---
# <a name="importing-kernel-mode-safe-integer-functions"></a>导入内核模式安全整数函数


内核模式安全整数函数都可用作在 ntintsafe.h 或链接到代码库中包含的内联代码。 Windows Driver Kit (WDK) 中提供了此标头文件。

请务必注意，您必须使用无符号值的算术运算。 若要使用的符号的值，必须使用转换函数将首先有符号的值转换为无符号值安全地使用算术函数之前。

## <a name="to-use-the-inline-versions-of-the-kernel-mode-safe-integer-functions"></a>若要使用的内核模式安全整数函数内联版本


包括标头文件，如所示。

```ManagedCPlusPlus
#include <ntintsafe.h>
```

 

 




