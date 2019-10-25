---
title: Bug 检查 0x6 INVALID_PROCESS_DETACH_ATTEMPT
description: INVALID_PROCESS_DETACH_ATTEMPT bug 检查的值为0x00000006。 此 bug 检查很少出现。
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
ms.openlocfilehash: a2da0ddc9b2d0032f789793602b9e282d608fe5b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72826999"
---
# <a name="bug-check-0x6-invalid_process_detach_attempt"></a>Bug 检查0x6：\_分离\_尝试无效\_进程


\_分离\_尝试 bug 检查的无效\_进程的值为0x00000006。

此 bug 检查很少出现。 此 bug 检查可能由以下原因引起：调用 [**KeStackAttachProcess**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-kestackattachprocess)例程，并随后在[**PLOAD_IMAGE_NOTIFY_ROUTINE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nc-ntddk-pload_image_notify_routine)回调函数的驱动程序实现中调用[**KeUnstackDetachProcess**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-keunstackdetachprocess) 。 回调在已加载映像的进程的线程中运行。

> [!IMPORTANT]
> 本主题面向程序员。 如果你是在使用计算机时收到蓝屏错误代码的客户，请参阅[排查蓝屏错误](https://www.windows.com/stopcode)。


 

 




