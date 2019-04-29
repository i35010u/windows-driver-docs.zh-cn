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
ms.openlocfilehash: 431e3f54f6bb397f0b25c72998720767c28ba614
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63354701"
---
# <a name="bug-check-0x128-workerthreadreturnedwithbadiopriority"></a>Bug 检查 0x128：辅助角色\_线程\_返回\_WITH\_错误\_IO\_优先级


辅助角色\_线程\_返回\_WITH\_错误\_IO\_优先级 bug 检查的值为 0x00000128。 这指示工作线程 IOPriority 已错误地修改由被调用的辅助角色例程。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。


## <a name="workerthreadreturnedwithbadiopriority-parameters"></a>辅助角色\_线程\_返回\_WITH\_错误\_IO\_优先级参数


| 参数 | 描述                                                                                                                                             |
|-----------|---------------------------------------------------------------------------------------------------------------------------------------------------------|
| 1         | 工作线程例程的地址 (使用[ **ln （列表最接近符号）** ](ln--list-nearest-symbols-.md)命令此地址来查找有问题的驱动程序) |
| 2         | 当前 IoPrioirity 值                                                                                                                               |
| 3         | 工作项参数                                                                                                                                      |
| 4         | 工作项地址                                                                                                                                        |

 

 

 




