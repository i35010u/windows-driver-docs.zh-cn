---
title: Bug 检查 0x102 DPC_WATCHDOG_TIMEOUT
description: DPC_WATCHDOG_TIMEOUT bug 检查具有 0x00000102 值。 这表示在分配的时间间隔内未执行 DPC 监视程序例程。
ms.assetid: 1BEC2701-3127-4FB9-AD0F-DD54A9F2C2C3
keywords:
- Bug 检查 0x102 DPC_WATCHDOG_TIMEOUT
- DPC_WATCHDOG_TIMEOUT
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- DPC_WATCHDOG_TIMEOUT
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 5076be370f5280ddf722221994f528a9f0ad5243
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67362367"
---
# <a name="bug-check-0x102-dpcwatchdogtimeout"></a>Bug 检查 0x102：DPC\_监视器\_超时


DPC\_监视器\_超时错误检查的值为 0x00000102。 这表示在分配的时间间隔内未执行 DPC 监视程序例程。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://support.microsoft.com/help/14238/windows-10-troubleshoot-blue-screen-errors)。


## <a name="dpcwatchdogtimeout-parameters"></a>DPC\_监视器\_超时参数


| 参数 | 描述                                            |
|-----------|--------------------------------------------------------|
| 1         | 在名义上的时钟计时周期中的 DPC 监视器超时时间间隔。 |
| 2         | 挂起处理器 PRCB 地址。                |
| 3         | 保留                                               |
| 4         | 保留                                               |

 

<a name="cause"></a>原因
-----

检查此错误通常意味着，在时钟级别及调度级别以上的 IRQL 挂起 ISR 或 DPC 例程挂起指定的处理器上。

例如有关 StorPort 微型端口驱动程序，StorPort.sys 处理 I/O 完成例程在调度运行中的\_级别，按顺序调用刚刚完成的所有 Irp 的 I/O 完成例程。 如果 I/O 完成例程单独或一起需要很长时间，键盘和/或鼠标可能会停止响应。 还有可能 Windows DPC 监视器计时器例程将决定 StorPort 例程已过多的时间才能完成。

<a name="resolution"></a>分辨率
----------

存储堆栈中的内核驱动程序通过高效编码的驱动程序的 I/O 完成例程可以减少问题的可能性。 如果仍不可以执行所有必要的处理，在完成例程中有足够的时间，例程可以创建多个 I/O 工作的工作元素、 排队到工作队列的元素和状态\_详细\_处理\_必选项;工作线程的驱动程序应找到工作元素、 执行工作和执行操作以确保 IRP 的更多的 I/O 处理 IRP 的 IoCallerDriver。

 

 




