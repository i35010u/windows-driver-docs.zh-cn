---
title: Bug 检查 0x166 CLUSTER_RESOURCE_CALL_TIMEOUT_LIVEDUMP
description: CLUSTER_RESOURCE_CALL_TIMEOUT_LIVEDUMP bug 检查具有 0x00000166 值。 这指示群集资源调用所花时间超过配置的超时值。
keywords:
- Bug 检查 0x166 CLUSTER_RESOURCE_CALL_TIMEOUT_LIVEDUMP
- CLUSTER_RESOURCE_CALL_TIMEOUT_LIVEDUMP
ms.date: 12/27/2018
topic_type:
- apiref
api_name:
- CLUSTER_RESOURCE_CALL_TIMEOUT_LIVEDUMP
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: bdafef3629723d70a3aef3416f824d73c71a0484
ms.sourcegitcommit: ece0a2affa08f1b6446368ede06040b3153aaae2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/23/2019
ms.locfileid: "56743512"
---
# <a name="bug-check-0x166-clusterresourcecalltimeoutlivedump"></a>Bug 检查 0x166:群集\_资源\_调用\_超时\_LIVEDUMP

群集\_资源\_调用\_超时\_LIVEDUMP bug 检查的值为 0x00000166。 这指示群集资源调用所花时间超过配置的超时值。

**重要**本主题适用于程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。


## <a name="clusterresourcecalltimeoutlivedump-parameters"></a>群集\_资源\_调用\_超时\_LIVEDUMP 参数

|参数|描述|
|--- |--- |
|1|资源主机监视器 PID。|
|2|处理资源调用的线程 TID。|
|3|资源调用类型-下面列出。|
|4|子代码。 当参数 3 等于 8，则此参数包含群集资源的控制代码。 当参数 3 等于 9，则此参数包含群集资源类型控制代码。|

**资源调用类型**

    1  OPEN
    2  CLOSE
    3  ONLINE
    4  OFFLINE
    5  TERMINATE
    6  ARBITRATE
    7  RELEASE
    8  RESOURCE CONTROL
    9  RESOURCE TYPE CONTROL
    10 LOOKS ALIVE
    11 IS ALIVE
    12 FAILURE NOTIFICATION
    13 SHUTDOWN PROCESS
    14 CANCEL


## <a name="cause"></a>原因
-----

群集资源调用花的时间超过配置的超时。 系统生成的转储实时的分析的延迟。

（此代码可以永远不会用于实际的执行错误检查。）

## <a name="resolution"></a>分辨率
----------
 

## <a name="see-also"></a>请参阅
----------

[故障排除挂起使用实时转储 （博客）](https://blogs.msdn.microsoft.com/clustering/2016/03/02/troubleshooting-hangs-using-live-dump/)

[Bug 检查代码参考](bug-check-code-reference2.md)




