---
title: Bug 检查 0x1D2 WORKER_THREAD_INVALID_STATE
description: WORKER_THREAD_INVALID_STATE bug 检查的值为0x000001D2。
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
ms.openlocfilehash: 1075d939b592b53653f07cc29aeaafe3314747d7
ms.sourcegitcommit: 2f37e8de9759164804a3b1c7f5c9e497a607539b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/26/2020
ms.locfileid: "83851564"
---
# <a name="bug-check-0x1d2-worker_thread_invalid_state"></a>Bug 检查0x1D2：工作 \_ 线程 \_ 无效 \_ 状态 

> [!IMPORTANT]
> 本主题适用于程序员。 如果你是在使用计算机时收到蓝屏错误代码的客户，请参阅[排查蓝屏错误](https://www.windows.com/stopcode)。


工作 \_ 线程的 \_ \_ 状态 bug 检查无效，其值为0x000001D2。 

此错误表示执行工作线程处于无效状态。

## <a name="worker_thread_invalid_state-parameters"></a>工作 \_ 线程 \_ 无效的 \_ 状态参数

参数 | 说明 
|---------|--------------|
1 | 失败类型
2 | 工作线程的地址
3 | 保留
4 | 保留



**参数1值**

  0x0：正在终止进程的工作线程具有未完成的 i/o
  
  2-工作线程的地址
  
  3-保留
  
  4-保留
