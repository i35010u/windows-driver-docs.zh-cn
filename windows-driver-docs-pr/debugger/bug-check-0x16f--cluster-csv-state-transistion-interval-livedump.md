---
title: Bug 检查 0x16F CLUSTER_CSV_STATE_TRANSITION_INTERVAL_TIMEOUT_LIVEDUMP
description: CLUSTER_CSV_STATE_TRANSITION_INTERVAL_TIMEOUT_LIVEDUMP bug 检查具有 0x0000016F 值。 这表示群集共享卷下一个状态转换请求仍未送达。
keywords:
- Bug 检查 0x16F CLUSTER_CSV_STATE_TRANSITION_INTERVAL_TIMEOUT_LIVEDUMP
- CLUSTER_CSV_STATE_TRANSITION_INTERVAL_TIMEOUT_LIVEDUMP
ms.date: 01/03/2019
topic_type:
- apiref
api_name:
- CLUSTER_CSV_STATE_TRANSITION_INTERVAL_TIMEOUT_LIVEDUMP
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 135a66a5a7933e8bda6cae8c34bad6757be286a4
ms.sourcegitcommit: ece0a2affa08f1b6446368ede06040b3153aaae2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/23/2019
ms.locfileid: "56743511"
---
# <a name="bug-check-0x16f-clustercsvstatetransitionintervaltimeoutlivedump"></a>Bug 检查 0x16F:群集\_CSV\_状态\_过渡\_间隔\_超时\_LIVEDUMP

群集\_CSV\_状态\_过渡\_间隔\_超时\_LIVEDUMP bug 检查的值为 0x0000016F。 这表示群集共享卷下一个状态转换请求仍未送达。

**重要**本主题适用于程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。


## <a name="clustercsvstatetransitionintervaltimeoutlivedump-parameters"></a>群集\_CSV\_状态\_过渡\_间隔\_超时\_LIVEDUMP 参数


|参数|描述|
|--- |--- |
|1| 群集服务 PID。|
|2| CSV 目标状态 Id-下面列出。 |
|3| 保留 |
|4| 保留 |


**CSV 目标状态 Id**

     0  Waiting for volume to transition to the Init state. 
     1  Waiting for volume to transition to the Paused state. 
     2  Waiting for volume to transition to the Draining state. 
     3  Waiting for volume to transition to the Set-Down-Level state. 
     4  Waiting for volume to transition to the Active state.


## <a name="cause"></a>原因
-----

群集共享卷的下一个状态转换请求仍未送达。

系统生成的转储实时的分析的延迟。

（此代码可以永远不会用于实际的执行错误检查。）


## <a name="resolution"></a>分辨率
----------
 

## <a name="see-also"></a>请参阅
----------

[故障排除挂起使用实时转储 （博客）](https://blogs.msdn.microsoft.com/clustering/2016/03/02/troubleshooting-hangs-using-live-dump/)

[Bug 检查代码参考](bug-check-code-reference2.md)




