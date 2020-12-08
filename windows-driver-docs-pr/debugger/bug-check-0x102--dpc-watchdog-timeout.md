---
title: Bug 检查 0x102 DPC_WATCHDOG_TIMEOUT
description: DPC_WATCHDOG_TIMEOUT bug 检查的值为0x00000102。 这表示未在分配的时间间隔内执行 DPC 监视程序例程。
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
ms.openlocfilehash: 0d79dabb66c75658f287c146d645b9c66a6b4785
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96817571"
---
# <a name="bug-check-0x102-dpc_watchdog_timeout"></a>Bug 检查0x102： DPC \_ 监视程序 \_ 超时


DPC \_ 监视程序 \_ 超时 bug 检查的值为0x00000102。 这表示未在分配的时间间隔内执行 DPC 监视程序例程。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="dpc_watchdog_timeout-parameters"></a>DPC \_ 监视程序 \_ 超时参数


| 参数 | 描述                                            |
|-----------|--------------------------------------------------------|
| 1         | DPC 监视程序的时间间隔（以标称时钟计时周期）。 |
| 2         | 挂起的处理器的 PRCB 地址。                |
| 3         | 预留                                               |
| 4         | 预留                                               |

 

<a name="cause"></a>原因
-----

此 bug 检查通常表示 ISR 挂起于低于时钟级别和高于调度级别的 IRQL，或在指定的处理器上挂起了 DPC 例程。

例如，对于 StorPort 微型端口驱动程序，StorPort.sys 处理在调度级别运行的例程中的 i/o 完成， \_ 并按顺序调用刚刚完成的所有 irp 的 i/o 完成例程。 如果单个或多个 i/o 完成例程需要很长时间，则键盘和/或鼠标可能会停止响应。 此外，Windows DPC 监视程序计时器例程还可能会确定 StorPort 例程已花了很多时间才能完成。

<a name="resolution"></a>解决方法
----------

存储堆栈中的内核驱动程序可以通过高效地编码驱动程序的 i/o 完成例程来减少问题的可能性。 如果在完成例程中仍无法完成所有必要的处理，则为。例程可以为 i/o 工作创建一个工作元素，将元素排队到工作队列，并返回 \_ 所需的状态更多 \_ \_ ; 然后，驱动程序的工作线程应找到工作元素，为 irp 执行工作并执行 IoCallerDriver，以确保 irp 的后续 i/o 处理。

 

 




