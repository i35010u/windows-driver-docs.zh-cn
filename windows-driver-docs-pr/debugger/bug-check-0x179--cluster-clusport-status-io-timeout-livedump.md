---
title: Bug 检查 0x179 CLUSTER_CLUSPORT_STATUS_IO_TIMEOUT_LIVEDUMP
description: CLUSTER_CLUSPORT_STATUS_IO_TIMEOUT_LIVEDUMP bug 检查具有 0x00000179 值。 这表示发起程序节点上的 SMB 客户端会指出目标节点上的 IO 时间太长并且失败的 STATUS_IO_TIMEOUT 所有 Io。
keywords:
- Bug 检查 0x179 CLUSTER_CLUSPORT_STATUS_IO_TIMEOUT_LIVEDUMP
- CLUSTER_CLUSPORT_STATUS_IO_TIMEOUT_LIVEDUMP
ms.date: 01/03/2019
topic_type:
- apiref
api_name:
- CLUSTER_CLUSPORT_STATUS_IO_TIMEOUT_LIVEDUMP
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: fa1d96f00ba7ac61a9b63208be9a20bd3a1e04e6
ms.sourcegitcommit: d03b44343cd32b3653d0471afcdd3d35cb800c0d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2019
ms.locfileid: "67519888"
---
# <a name="bug-check-0x179-clusterclusportstatusiotimeoutlivedump"></a>Bug 检查 0x179：群集\_CLUSPORT\_状态\_IO\_超时\_LIVEDUMP

群集\_CLUSPORT\_状态\_IO\_超时\_LIVEDUMP bug 检查的值为 0x00000179。 这表示发起程序节点上的 SMB 客户端错误报告到目标节点的 IO 时间太长并且失败的 STATUS_IO_TIMEOUT 所有 Io。



> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://www.windows.com/stopcode)。



## <a name="clusterclusportstatusiotimeoutlivedump-parameters"></a>群集\_CLUSPORT\_状态\_IO\_超时\_LIVEDUMP 参数

|参数|描述|
|--- |--------------- |
|1| 遇到超时的 IRP。|
|2| 保留。 |
|3| 保留。 |
|4| 保留。 |


## <a name="cause"></a>原因
-----

发起程序节点上的 SMB 客户端会指出目标节点上的 IO 时间太长并且失败的 STATUS_IO_TIMEOUT 所有 Io。

响应，群集发起程序捕获发起程序节点上的实时转储，以便我们可以分析什么 IO 花费的时间。

在转储的辅助数据的流提供了其他信息。

（此代码可以永远不会用于实际的执行错误检查。）


## <a name="resolution"></a>分辨率
----------
 

## <a name="see-also"></a>请参阅
----------

[故障排除挂起使用实时转储 （博客）](https://techcommunity.microsoft.com/t5/Failover-Clustering/bg-p/FailoverClustering)

[Bug 检查代码参考](bug-check-code-reference2.md)




