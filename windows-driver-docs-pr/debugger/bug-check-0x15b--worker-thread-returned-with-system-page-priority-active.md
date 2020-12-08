---
title: Bug 检查 0x15B WORKER_THREAD_RETURNED_WITH_SYSTEM_PAGE_PRIORITY_ACTIVE
description: WORKER_THREAD_RETURNED_WITH_SYSTEM_PAGE_PRIORITY_ACTIVE bug 检查的值为0x0000015B，指示工作线程的系统页优先级已泄漏。
keywords:
- Bug 检查 0x15B WORKER_THREAD_RETURNED_WITH_SYSTEM_PAGE_PRIORITY_ACTIVE
- WORKER_THREAD_RETURNED_WITH_SYSTEM_PAGE_PRIORITY_ACTIVE
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- WORKER_THREAD_RETURNED_WITH_SYSTEM_PAGE_PRIORITY_ACTIVE
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 2b6f6de37344deae44ab7036710546aca96fe901
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96830797"
---
# <a name="bug-check-0x15b-worker_thread_returned_with_system_page_priority_active"></a>Bug 检查0x15B： \_ \_ 返回的工作线程 \_ 的 \_ 系统 \_ 页优先级为 \_ \_ 活动


返回的 \_ 工作 \_ 线程 \_ 具有 \_ 系统 \_ 页 \_ 优先级 \_ 活动 bug 检查的值为0x0000015B。 这表明，工作线程的系统页面优先级已被调用的辅助角色泄露。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="worker_thread_returned_with_system_page_priority_active-parameters"></a>\_ \_ 返回的工作线程 \_ 具有 \_ 系统 \_ 页 \_ 优先级 \_ 活动参数


| 参数 | 描述                                                                    |
|-----------|--------------------------------------------------------------------------------|
| 1         | 辅助角色例程的地址 (在此地址上执行 ln，以查找有问题的驱动程序)  |
| 2         | 当前系统页优先级值                                             |
| 3         | 工作项参数                                                             |
| 4         | 工作项地址                                                               |

 

 

 




