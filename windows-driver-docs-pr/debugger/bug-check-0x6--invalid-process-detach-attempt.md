---
title: Bug 检查 0x6 INVALID_PROCESS_DETACH_ATTEMPT
description: INVALID_PROCESS_DETACH_ATTEMPT bug 检查具有值为 0x00000006。 检查此错误极少出现。
ms.assetid: f468b348-6576-4430-aa8f-b6100a689fee
keywords:
- Bug 检查 0x6 INVALID_PROCESS_DETACH_ATTEMPT
- INVALID_PROCESS_DETACH_ATTEMPT
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- INVALID_PROCESS_DETACH_ATTEMPT
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 0d17c01b7ed232768e85e4a67aaa23668761141f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63366466"
---
# <a name="bug-check-0x6-invalidprocessdetachattempt"></a>Bug 检查 0x6：无效\_进程\_分离\_尝试


无效\_进程\_分离\_尝试错误检查的值为 0x00000006。

检查此错误极少出现。 此 bug 检查可能导致通过调用 [**KeStackAttachProcess** ](https://msdn.microsoft.com/library/windows/hardware/ff549659)例程并随后调用[ **KeUnstackDetachProcess** ](https://msdn.microsoft.com/library/windows/hardware/ff549677)中的驱动程序的实现[ **PLOAD_IMAGE_NOTIFY_ROUTINE** ](https://msdn.microsoft.com/library/windows/hardware/mt764088(v=vs.85).aspx)回调函数。 在回调过程加载图像的线程中运行。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。


 

 




