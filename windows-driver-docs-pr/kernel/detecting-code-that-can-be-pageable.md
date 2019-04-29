---
title: 检测可分页的代码
description: 检测可分页的代码
ms.assetid: 5e8a021d-09c3-4e63-b5a8-7559c384ae3d
keywords:
- 可分页的驱动程序 WDK 内核，代码检测
- 检测可分页的代码
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: a983aa1423e40664010c813f26ef8a12c82eebdc
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63388180"
---
# <a name="detecting-code-that-can-be-pageable"></a>检测可分页的代码





若要检测的 IRQL 在运行的代码&gt;= 调度\_级别，使用[ **PAGED\_代码**](https://msdn.microsoft.com/library/windows/hardware/ff558773)宏。 在调试模式下，此宏生成一条消息，当代码运行在 IRQL &gt;= 调度\_级别。 若要将标记为分页代码，如以下示例所示的整个例程的例程中的第一个语句添加该宏：

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

若要确保你在进行这正确，请运行[Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff545448)针对与您已完成的驱动程序**强制 IRQL 检查**选项处于启用状态。 此选项将导致系统自动出可分页的所有代码页对驱动程序引发调度到的 IRQL 每次\_级别或更高版本。 使用驱动程序验证程序，您可以迅速找到驱动程序的任何 bug 在此区域中。 否则为通常将仅由客户发现这些 bug，并且它们可以经常是非常困难，以便重现。

 

 




