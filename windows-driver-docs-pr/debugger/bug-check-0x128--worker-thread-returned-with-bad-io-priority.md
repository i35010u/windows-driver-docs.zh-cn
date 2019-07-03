---
title: Bug 检查 0x128 WORKER_THREAD_RETURNED_WITH_BAD_IO_PRIORITY
description: WORKER_THREAD_RETURNED_WITH_BAD_IO_PRIORITY bug 检查具有 0x00000128 值。 这指示工作线程 IOPriority 已错误地修改由被调用的辅助角色例程。
ms.assetid: 2659491F-2257-4553-A7A4-ECA39DD0A0F7
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
ms.openlocfilehash: 0f0d852cdef58edbe655535fef4cb0f46477b120
ms.sourcegitcommit: d03b44343cd32b3653d0471afcdd3d35cb800c0d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2019
ms.locfileid: "67520705"
---
# <a name="bug-check-0x128-workerthreadreturnedwithbadiopriority"></a>Bug 检查 0x128：辅助角色\_线程\_返回\_WITH\_错误\_IO\_优先级


辅助角色\_线程\_返回\_WITH\_错误\_IO\_优先级 bug 检查的值为 0x00000128。 这指示工作线程 IOPriority 已错误地修改由被调用的辅助角色例程。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://www.windows.com/stopcode)。


## <a name="workerthreadreturnedwithbadiopriority-parameters"></a>辅助角色\_线程\_返回\_WITH\_错误\_IO\_优先级参数


| 参数 | 描述                                                                                                                                             |
|-----------|---------------------------------------------------------------------------------------------------------------------------------------------------------|
| 1         | 工作线程例程的地址 (使用[ **ln （列表最接近符号）** ](ln--list-nearest-symbols-.md)命令此地址来查找有问题的驱动程序) |
| 2         | 当前 IoPrioirity 值                                                                                                                               |
| 3         | 工作项参数                                                                                                                                      |
| 4         | 工作项地址                                                                                                                                        |

 

 

 




