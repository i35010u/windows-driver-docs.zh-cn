---
title: Bug 检查 0x4000008A THREAD_TERMINATE_HELD_MUTEX
description: THREAD_TERMINATE_HELD_MUTEX bug 检查具有 0x4000008A 值。
ms.assetid: 30A796F0-D622-43F2-8050-C9B62941FBE9
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
ms.openlocfilehash: 62e9359c862b7c3be1d7b599ce8d133aac503719
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2019
ms.locfileid: "59903273"
---
# <a name="bug-check-0x4000008a-threadterminateheldmutex"></a>Bug 检查 0x4000008A：线程\_TERMINATE\_保持\_互斥体


在线程\_TERMINATE\_保持\_互斥体 bug 检查的值为 0x4000008A。 这指示一个驱动程序获取互斥体已退出之前无法释放互斥体的线程上。 这可能导致由驱动程序返回到用户模式而未释放互斥体或由驱动程序获取互斥体，并且，然后引发异常会导致，正在终止运行的线程。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。


## <a name="threadterminateheldmutex-parameters"></a>线程\_TERMINATE\_保持\_互斥体参数


| 参数 | 描述                                      |
|-----------|--------------------------------------------------|
| 1         | 拥有 KMUTEX KTHREAD 的地址。 |
| 2         | 拥有 KMUTEX 的地址。         |
| 3         | 保留                                         |
| 4         | 保留                                         |

 

<a name="cause"></a>原因
-----

若要调查，请查看调用堆栈。 如果没有直接跟系统异常处理例程在堆栈上的驱动程序，然后线程终止例程，此驱动程序位于容错域和需要进行修复，以便它不会导致同时保留内核互斥体未处理的异常。 如果堆栈只是显示正常线程终止代码，并且其中涉及任何驱动程序，运行[ **！ 池**](-pool.md) ，或使用[ **ln （列表最接近符号）** ](ln--list-nearest-symbols-.md)互斥体 （参数 2） 和查看是否有可以发现谁拥有它的地址。 此 bug 几乎肯定会在该互斥体的所有者的代码中。

 

 




