---
title: Bug 检查 0x19A WORKER_THREAD_RETURNED_WHILE_ATTACHED_TO_SILO
description: WORKER_THREAD_RETURNED_WHILE_ATTACHED_TO_SILO bug 检查具有 0x0000019A 值。 这表示一个工作线程附加到接收器，并返回之前未分离。
ms.assetid: D947FF20-4C86-4879-A5CA-934A20BE61C9
keywords:
- Bug 检查 0x19A WORKER_THREAD_RETURNED_WHILE_ATTACHED_TO_SILO
- WORKER_THREAD_RETURNED_WHILE_ATTACHED_TO_SILO
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- WORKER_THREAD_RETURNED_WHILE_ATTACHED_TO_SILO
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 1b99892a9d0f5daedbf77209d2fb9917c1008c77
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63352450"
---
# <a name="bug-check-0x19a-workerthreadreturnedwhileattachedtosilo"></a>Bug 检查 0x19A：辅助角色\_线程\_返回\_虽然\_附加\_TO\_接收器


辅助角色\_线程\_返回\_虽然\_附加\_TO\_接收器 bug 检查的值为 0x0000019A。 这表示一个工作线程附加到接收器，并返回之前未分离。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。


## <a name="workerthreadreturnedwhileattachedtosilo-parameters"></a>辅助角色\_线程\_返回\_虽然\_附加\_TO\_接收器参数


| 参数 | 描述               |
|-----------|---------------------------|
| 1         | 工作线程例程的地址 |
| 2         | 工作项参数        |
| 3         | 工作项地址          |
| 4         | 保留                  |

 

<a name="cause"></a>原因
-----

若要调查是否可以使用[ **ln （列表最接近符号）**](ln--list-nearest-symbols-.md)命令参数 1，以帮助确定错误运行正常的驱动程序。

 

 




