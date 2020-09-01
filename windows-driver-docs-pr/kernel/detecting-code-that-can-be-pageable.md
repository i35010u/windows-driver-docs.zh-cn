---
title: 检测可分页的代码
description: 检测可分页的代码
ms.assetid: 5e8a021d-09c3-4e63-b5a8-7559c384ae3d
keywords:
- 可分页驱动程序 WDK 内核，代码检测
- 检测可分页代码
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 14ef84a6ec9a667e441856fc16697fd03a79a4f3
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89189079"
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

若要确保正确执行此操作，请在启用了 "**强制 IRQL 检查**" 选项的情况下针对完成的驱动程序运行[驱动程序验证程序](../devtest/driver-verifier.md)。 此选项使系统在每次驱动程序将 IRQL 提升为调度 \_ 级别或更高级别时，自动将所有可分页的代码分页。 使用驱动程序验证程序，可以快速找到此区域中的任何驱动程序错误。 否则，这些 bug 通常仅由客户发现，它们可能会很难重现。

 

