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
ms.openlocfilehash: 9b05871743c47aaca53dd42dc5dd8575bccbd73c
ms.sourcegitcommit: fb8b1d2e18dd727e8a479b04c9e6051e7e9fa484
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/18/2019
ms.locfileid: "59239138"
---
# <a name="bug-check-0x18c-hyperguardviolation"></a>Bug 检查 0x18C：HYPERGUARD\_冲突 

HYPERGUARD\_冲突错误检查的值为 0x0000018C。 这表示内核已检测到关键内核代码或数据已损坏。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。


> [!NOTE] 
> 此错误代码被保留供 Hyperguard 仅。  
> 它不是常规用途 bug 代码供数据损坏方案中的其他组件使用。  
> 相反，定义您的组件的唯一错误代码。   
> 在组件中不使用此 bug 的代码。
>

 ## <a name="hyperguardviolation-parameters"></a>HYPERGUARD\_冲突参数

| 参数 | 描述 |
|-----------|-------------|
| 1    | 类型的损坏区域-下面列出的值。 |
| 2    | 失败类型的相关信息。 |
| 3    | 保留。  |
| 4    | 保留。  |


**类型的损坏区域**

1001 :通用数据区域

1002 :页哈希不匹配

1004 :处理器 IDT

1005 :处理器 GDT

1007 :调试例程修改

1008 :动态代码区域

1009 :可共享的通用数据区域

100a:虚拟机监控程序覆盖区域

100b:处理器模式下配置不正确

100 c:扩展的处理器控制寄存器

100 d:安全的内存区域

100e:加载的模块

100f:处理器状态区域

1010 :内核 CFG 位图

1011 :虚拟地址 0 页

1012 :备用的倒排的函数表

1013 :按需页验证失败

1016 :安全映像区域

1017 :内核虚拟地址保护不一致

1101 :内部上下文损坏

1102 :IDTR 修改

1103 :GDTR 修改

## <a name="cause"></a>原因
-----

在内核检测到关键内核代码或数据已损坏时，将生成此错误检查。 通常有三个原因已损坏：

1) 驱动程序已意外或故意修改关键内核代码或数据。 

2) 开发人员尝试正常内核使用设置断点时引导系统未附加内核调试程序。 普通断点，"最佳实践"，如果在启动时附加调试器可以仅设置。 硬件断点，"ba"，可以随时设置。

3) 硬件损坏发生，例如失败 RAM 保存内核代码或数据。


## <a name="see-also"></a>请参阅
----------

[Bug 检查代码参考](bug-check-code-reference2.md)





