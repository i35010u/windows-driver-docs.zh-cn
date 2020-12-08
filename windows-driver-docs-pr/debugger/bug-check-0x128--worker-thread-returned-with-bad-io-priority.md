---
title: Bug 检查 0x128 WORKER_THREAD_RETURNED_WITH_BAD_IO_PRIORITY
description: WORKER_THREAD_RETURNED_WITH_BAD_IO_PRIORITY bug 检查的值为0x00000128。 这表示调用的辅助角色 IOPriority 错误地修改了工作线程。
keywords:
- Bug 检查 0x128 WORKER_THREAD_RETURNED_WITH_BAD_IO_PRIORITY
- WORKER_THREAD_RETURNED_WITH_BAD_IO_PRIORITY
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- WORKER_THREAD_RETURNED_WITH_BAD_IO_PRIORITY
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: a4c3fe84842d27c8070ac22db745be239cc174dd
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96818661"
---
# <a name="bug-check-0x128-worker_thread_returned_with_bad_io_priority"></a>Bug 检查0x128： \_ \_ 返回的工作线程 \_ 具有 \_ 错误的 \_ IO \_ 优先级


\_ \_ \_ 使用 \_ 错误 \_ \_ 的 IO 优先级 bug 检查返回的工作线程的值为0x00000128。 这表示调用的辅助角色 IOPriority 错误地修改了工作线程。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="worker_thread_returned_with_bad_io_priority-parameters"></a>\_ \_ 返回的工作 \_ 线程 \_ 包含错误的 \_ IO \_ 优先级参数


| 参数 | 描述                                                                                                                                             |
|-----------|---------------------------------------------------------------------------------------------------------------------------------------------------------|
| 1         | 辅助进程例程的地址 (使用此地址上与 [**ln (列表最近的符号)**](ln--list-nearest-symbols-.md) 命令查找有问题的驱动程序)  |
| 2         | 当前 IoPrioirity 值                                                                                                                               |
| 3         | 工作项参数                                                                                                                                      |
| 4         | 工作项地址                                                                                                                                        |

 

 

 




