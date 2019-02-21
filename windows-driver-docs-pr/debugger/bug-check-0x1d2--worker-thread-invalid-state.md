---
title: Bug 检查 0x1D2 WORKER_THREAD_INVALID_STATE
description: WORKER_THREAD_INVALID_STATE bug 检查具有 0x000001D2 值。
keywords:
- Bug 检查 0x1D2 WORKER_THREAD_INVALID_STATE
- WORKER_THREAD_INVALID_STATE
ms.date: 05/23/2018
topic_type:
- apiref
api_name:
- WORKER_THREAD_INVALID_STATE
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c45f39760f278e31966d8569e3befb2ae63fccd7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547339"
---
# <a name="bug-check-bug-check-0x1d2-workerthreadinvalidstate"></a>Bug 检查 Bug 检查 0x1D2:辅助角色\_线程\_无效\_状态 

**重要**本主题适用于程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。

辅助角色\_线程\_无效\_状态 bug 检查的值为 0x000001D2。 

此错误表示 executive 工作线程处于无效状态。

## <a name="workerthreadinvalidstate-parameters"></a>辅助角色\_线程\_无效\_状态参数

参数 | 描述 
|---------|--------------|
1 | 失败的类型
2 | 工作线程地址
3 | 保留
4 | 保留



**参数 1 的值**

  0x0:工作线程终止的过程中具有未完成 I/O
  
  2-的工作线程地址
  
  3-保留
  
  4-保留
