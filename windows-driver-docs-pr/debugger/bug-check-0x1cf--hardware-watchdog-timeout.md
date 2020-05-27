---
title: Bug 检查 0x1CF HARDWARE_WATCHDOG_TIMEOUT
description: HARDWARE_WATCHDOG_TIMEOUT bug 检查的值为0x000001CF。
keywords:
- Bug 检查 0x1CF HARDWARE_WATCHDOG_TIMEOUT
- HARDWARE_WATCHDOG_TIMEOUT
ms.date: 05/23/2018
topic_type:
- apiref
api_name:
- HARDWARE_WATCHDOG_TIMEOUT
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: dbb23fa28b453adbe964cf9d0c0ac777bb988916
ms.sourcegitcommit: 2f37e8de9759164804a3b1c7f5c9e497a607539b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/26/2020
ms.locfileid: "83851984"
---
# <a name="bug-check-0x1cf-hardware_watchdog_timeout"></a>Bug 检查0x1CF：硬件 \_ 监视器 \_ 超时 

> [!IMPORTANT]
> 本主题适用于程序员。 如果你是在使用计算机时收到蓝屏错误代码的客户，请参阅[排查蓝屏错误](https://www.windows.com/stopcode)。


HARDWARE_WATCHDOG_TIMEOUT bug 检查的值为0x000001CF。 这表示系统挂起，未处理计时器时钟周期。


## <a name="hardware_watchdog_timeout-parameters"></a>硬件 \_ 监视程序 \_ 超时参数
 
参数 | 说明 
|---------|--------------|
1 | 上次重置监视程序的时间，以中断时间为间隔。
2 | 当前中断时间。
3 | 当前的 QPC 时间戳。
4 | 时钟处理器的索引。


 

 




