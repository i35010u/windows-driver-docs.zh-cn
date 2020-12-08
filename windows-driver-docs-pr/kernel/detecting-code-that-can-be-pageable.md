---
title: 检测可分页的代码
description: 检测可分页的代码
keywords:
- 可分页驱动程序 WDK 内核，代码检测
- 检测可分页代码
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: e7afcb496dce0f66b93f993c36cb13389a29359c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96829563"
---
# <a name="detecting-code-that-can-be-pageable"></a>检测可分页的代码





若要检测以 IRQL &gt; = 调度级别运行的代码 \_ ，请使用 [**分页 \_ 代码**](./mm-bad-pointer.md) 宏。 在调试模式下，如果代码以 IRQL = 调度级别运行，则此宏将生成一条消息 &gt; \_ 。 添加宏作为例程中的第一个语句，将整个例程标记为分页代码，如以下示例所示：

```cpp
NTSTATUS 
MyDriverXxx( 
    IN OUT PVOID ParseContext OPTIONAL, 
    OUT PHANDLE Handle 
    ) 
{ 
    NTSTATUS Status; 
 
    PAGED_CODE(); 
. 
. 
. 
} 
```

若要确保正确执行此操作，请在启用了 "**强制 IRQL 检查**" 选项的情况下针对完成的驱动程序运行 [驱动程序验证程序](../devtest/driver-verifier.md)。 此选项使系统在每次驱动程序将 IRQL 提升为调度 \_ 级别或更高级别时，自动将所有可分页的代码分页。 使用驱动程序验证程序，可以快速找到此区域中的任何驱动程序错误。 否则，这些 bug 通常仅由客户发现，它们可能会很难重现。

 

