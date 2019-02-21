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
ms.openlocfilehash: ac69b337d5c7ed351d54f5ff3459a712da785f5c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543326"
---
# <a name="bug-check-0x128-workerthreadreturnedwithbadiopriority"></a>Bug 检查 0x128:辅助角色\_线程\_返回\_WITH\_错误\_IO\_优先级


辅助角色\_线程\_返回\_WITH\_错误\_IO\_优先级 bug 检查的值为 0x00000128。 这指示工作线程 IOPriority 已错误地修改由被调用的辅助角色例程。

**重要**本主题适用于程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。

## <a name="workerthreadreturnedwithbadiopriority-parameters"></a>辅助角色\_线程\_返回\_WITH\_错误\_IO\_优先级参数


| 参数 | 描述                                                                                                                                             |
|-----------|---------------------------------------------------------------------------------------------------------------------------------------------------------|
| 1         | 工作线程例程的地址 (使用[ **ln （列表最接近符号）** ](ln--list-nearest-symbols-.md)命令此地址来查找有问题的驱动程序) |
| 2         | 当前 IoPrioirity 值                                                                                                                               |
| 3         | 工作项参数                                                                                                                                      |
| 4         | 工作项地址                                                                                                                                        |

 

 

 




