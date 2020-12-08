---
title: Bug 检查 0x6 INVALID_PROCESS_DETACH_ATTEMPT
description: INVALID_PROCESS_DETACH_ATTEMPT bug 检查的值为0x00000006。 此 bug 检查很少出现。
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
ms.openlocfilehash: 7a298623b2fa630e6f439243b253176b52f5ee6c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839171"
---
# <a name="bug-check-0x6-invalid_process_detach_attempt"></a>Bug 检查0x6： \_ 进程 \_ 分离 \_ 尝试无效


无效的 \_ 进程 \_ 分离 \_ 尝试 bug 检查的值为0x00000006。

此 bug 检查很少出现。 此 bug 检查可能由以下原因引起：调用 [**KeStackAttachProcess**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-kestackattachprocess)例程，并随后在驱动程序的 [**PLOAD_IMAGE_NOTIFY_ROUTINE**](/windows-hardware/drivers/ddi/ntddk/nc-ntddk-pload_image_notify_routine)回调函数实现中调用 [**KeUnstackDetachProcess**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-keunstackdetachprocess) 。 回调在已加载映像的进程的线程中运行。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


 

