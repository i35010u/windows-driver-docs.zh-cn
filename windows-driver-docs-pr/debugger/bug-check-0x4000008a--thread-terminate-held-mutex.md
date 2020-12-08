---
title: Bug 检查 0x4000008A THREAD_TERMINATE_HELD_MUTEX
description: THREAD_TERMINATE_HELD_MUTEX bug 检查的值为0x4000008A。
keywords:
- Bug 检查 0x4000008A THREAD_TERMINATE_HELD_MUTEX
- THREAD_TERMINATE_HELD_MUTEX
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- THREAD_TERMINATE_HELD_MUTEX
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 83a6841b81219f19197720dd2d8256d27be1590f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96787929"
---
# <a name="bug-check-0x4000008a-thread_terminate_held_mutex"></a>Bug 检查0x4000008A：线程 \_ 终止 \_ 持有 \_ 互斥体


线程 \_ 终止 \_ 持有 \_ 的互斥体 bug 检查的值为0x4000008A。 这表明驱动程序在释放 mutex 之前退出的线程上已获取互斥体。 这可能是由以下原因引起的：驱动程序在未释放互斥体或驱动程序获取互斥体时返回到用户模式，然后引发了导致其正在运行的线程终止的异常。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="thread_terminate_held_mutex-parameters"></a>线程 \_ 终止 \_ 持有的 \_ MUTEX 参数


| 参数 | 描述                                      |
|-----------|--------------------------------------------------|
| 1         | 拥有 KMUTEX 的 KTHREAD 的地址。 |
| 2         | 拥有的 KMUTEX 的地址。         |
| 3         | 预留                                         |
| 4         | 预留                                         |

 

<a name="cause"></a>原因
-----

若要进行调查，请查看调用堆栈。 如果堆栈上有一个驱动程序，该驱动程序直接跟随系统异常处理例程，然后是线程终止例程，则该驱动程序是错误的，需要修复，以便它不会在保存内核 mutex 时导致未经处理的异常。 如果堆栈只显示正常线程终止代码，但没有发觉的驱动程序，请运行 [**！ pool**](-pool.md) 或使用 Ln (列出互斥体 (参数 2) 的地址上的 [**最接近符号)**](ln--list-nearest-symbols-.md) ，并查看是否可以发现谁拥有该代码。 此 bug 几乎肯定会在该 mutex 的所有者的代码中。

 

 




