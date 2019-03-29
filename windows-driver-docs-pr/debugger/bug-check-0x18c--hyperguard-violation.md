---
title: Bug 检查 0x18C HYPERGUARD_VIOLATION
description: HYPERGUARD_VIOLATION bug 检查具有 0x0000018C 值。 它指示内核已检测到关键内核代码或数据已损坏。
keywords:
- Bug 检查 0x18C HYPERGUARD_VIOLATION
- HYPERGUARD_VIOLATION
ms.date: 01/04/2019
topic_type:
- apiref
api_name:
- HYPERGUARD_VIOLATION
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 7350bf0b98669a96b18ed13b99e01c942da91b82
ms.sourcegitcommit: ece0a2affa08f1b6446368ede06040b3153aaae2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/23/2019
ms.locfileid: "56743467"
---
# <a name="bug-check-0x18c-hyperguardviolation"></a>Bug 检查 0x18C:HYPERGUARD\_冲突 

HYPERGUARD\_冲突错误检查的值为 0x0000018C。 这表示内核已检测到关键内核代码或数据已损坏。

**重要**本主题适用于程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。

> [!NOTE] 
> 此错误代码被保留供 Hyperguard 仅。  
> 它不是常规用途 bug 代码供数据损坏方案中的其他组件使用。  
> 相反，定义您的组件的唯一错误代码。   
> 在组件中不使用此 bug 的代码。
>

 ## <a name="hyperguardviolation-parameters"></a>HYPERGUARD\_冲突参数

| 参数 | 描述 |
|-----------|-------------|
| 1         | 类型的损坏区域-下面列出的值。 |
| 2         | 失败类型的相关信息。 |
| 3         | 保留。  |
| 4         | 保留。  |


**类型的损坏区域**

     1001 : A generic data region
     1002 : A page hash mismatch
     1004 : A processor IDT
     1005 : A processor GDT
     1007 : Debug routine modification
     1008 : A dynamic code region
     1009 : A generic shareable data region
     100a : A hypervisor overlay region
     100b : A processor mode misconfiguration
     100c : An extended processor control register
     100d : A secure memory region
     100e : A loaded module
     100f : A processor state region
     1010 : The kernel CFG bitmap
     1011 : The virtual address 0 page
     1012 : The alternate inverted function table
     1013 : An on-demand page verification failed
     1016 : A secure image region
     1017 : Kernel virtual address protection inconsistency
     1101 : Internal context corruption
     1102 : IDTR modification
     1103 : GDTR modification



## <a name="cause"></a>原因
-----

在内核检测到关键内核代码或数据已损坏时，将生成此错误检查。 通常有三个原因已损坏：

1) 驱动程序已意外或故意修改关键内核代码或数据。 

2) 开发人员尝试正常内核使用设置断点时引导系统未附加内核调试程序。 普通断点，"最佳实践"，如果在启动时附加调试器可以仅设置。 硬件断点，"ba"，可以随时设置。

3) 硬件损坏发生，例如失败 RAM 保存内核代码或数据。


## <a name="see-also"></a>请参阅
----------

[Bug 检查代码参考](bug-check-code-reference2.md)





