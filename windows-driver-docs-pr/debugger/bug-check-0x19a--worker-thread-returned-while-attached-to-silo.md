---
title: Bug 检查 0x19A WORKER_THREAD_RETURNED_WHILE_ATTACHED_TO_SILO
description: WORKER_THREAD_RETURNED_WHILE_ATTACHED_TO_SILO bug 检查的值为0x0000019A。 这表示附加到接收器的工作线程未在返回前分离。
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
ms.openlocfilehash: aed80631d83748e673c7ec532e50fa47628cae92
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96825233"
---
# <a name="bug-check-0x19a-worker_thread_returned_while_attached_to_silo"></a>Bug 检查0x19A： \_ \_ \_ \_ 附加 \_ 到 \_ 接收器时返回的工作线程


\_ \_ \_ \_ 附加 \_ 到接收器 BUG 检查时返回的工作线程的 \_ 值为0x0000019A。 这表示附加到接收器的工作线程未在返回前分离。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="worker_thread_returned_while_attached_to_silo-parameters"></a>\_ \_ \_ \_ 附加 \_ 到 \_ 接收器参数时返回的工作线程


| 参数 | 描述               |
|-----------|---------------------------|
| 1         | 辅助角色例程的地址 |
| 2         | 工作项参数        |
| 3         | 工作项地址          |
| 4         | 预留                  |

 

<a name="cause"></a>原因
-----

若要调查使用 [**ln (列出参数1上最接近的符号)**](ln--list-nearest-symbols-.md)命令，帮助确定正常的驱动程序。

 

 




