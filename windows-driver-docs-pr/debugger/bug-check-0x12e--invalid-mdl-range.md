---
title: Bug 检查 0x12E INVALID_MDL_RANGE
description: INVALID_MDL_RANGE bug 检查的值为0x0000012E。
keywords:
- Bug 检查 0x12E INVALID_MDL_RANGE
- INVALID_MDL_RANGE
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- INVALID_MDL_RANGE
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 0e146ae88aa5138ac91e70cc7322bda33c3ad41e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839958"
---
# <a name="bug-check-0x12e-invalid_mdl_range"></a>Bug 检查0x12E：无效的 \_ MDL \_ 范围


无效的 \_ MDL \_ 范围 bug 检查的值为0x0000012E。 这表明驱动程序调用了 IoBuildPartialMdl ( # A1 函数并向其传递了一个 MDL 来映射源 MDL 的部分，但指定的虚拟地址范围超出了源 MDL 的范围。 这通常是驱动程序错误。

源和目标 MDLs 以及要映射的地址范围长度是 IoBuildPartialMdl ( # A1 函数的参数，即 ) 。

```cpp
IoBuildPartialMdl(
        IN PMDL SourceMdl,
        IN OUT PMDL TargetMdl,
        IN PVOID VirtualAddress,
        IN ULONG Length
```

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="invalid_mdl_range-parameters"></a>无效的 \_ MDL \_ 范围参数


| 参数 | 描述    |
|-----------|----------------|
| 1         | SourceMdl      |
| 2         | TargetMdl      |
| 3         | VirtualAddress |
| 4         | 长度         |

 

 

 




