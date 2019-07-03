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
ms.openlocfilehash: 6d7bb2571ca98a7ff192b5275b053b983d01576a
ms.sourcegitcommit: d03b44343cd32b3653d0471afcdd3d35cb800c0d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2019
ms.locfileid: "67519318"
---
# <a name="bug-check-0x6-invalidprocessdetachattempt"></a>Bug 检查 0x6：无效\_进程\_分离\_尝试


无效\_进程\_分离\_尝试错误检查的值为 0x00000006。

检查此错误极少出现。 此 bug 检查可能导致通过调用 [**KeStackAttachProcess** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-kestackattachprocess)例程并随后调用[ **KeUnstackDetachProcess** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-keunstackdetachprocess)中的驱动程序的实现[ **PLOAD_IMAGE_NOTIFY_ROUTINE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nc-ntddk-pload_image_notify_routine)回调函数。 在回调过程加载图像的线程中运行。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://www.windows.com/stopcode)。


 

 




