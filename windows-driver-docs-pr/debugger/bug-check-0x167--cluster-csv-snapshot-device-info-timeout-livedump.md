---
title: Bug 检查 0x167 CLUSTER_CSV_SNAPSHOT_DEVICE_INFO_TIMEOUT_LIVEDUMP
description: CLUSTER_CSV_SNAPSHOT_DEVICE_INFO_TIMEOUT_LIVEDUMP bug 检查具有 0x00000167 值。 这表示查询快照信息 volsnap 群集服务调用时间太长。
keywords:
- Bug 检查 0x167 CLUSTER_CSV_SNAPSHOT_DEVICE_INFO_TIMEOUT_LIVEDUMP
- CLUSTER_CSV_SNAPSHOT_DEVICE_INFO_TIMEOUT_LIVEDUMP
ms.date: 01/03/2019
topic_type:
- apiref
api_name:
- CLUSTER_CSV_SNAPSHOT_DEVICE_INFO_TIMEOUT_LIVEDUMP
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 69bff42db35873b9a84a6bfac6d9b37aa7dfce62
ms.sourcegitcommit: d03b44343cd32b3653d0471afcdd3d35cb800c0d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2019
ms.locfileid: "67519960"
---
# <a name="bug-check-0x167-clustercsvsnapshotdeviceinfotimeoutlivedump"></a>Bug 检查 0x167：CLUSTER\_CSV\_SNAPSHOT\_DEVICE\_INFO\_TIMEOUT\_LIVEDUMP

群集\_CSV\_快照\_设备\_信息\_超时\_LIVEDUMPP bug 检查的值为 0x00000167。 这表示查询快照信息 volsnap 群集服务调用时间太长。


> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://www.windows.com/stopcode)。



## <a name="clustercsvsnapshotdeviceinfotimeoutlivedump-parameters"></a>群集\_CSV\_快照\_设备\_信息\_超时\_LIVEDUMP 参数

|参数|描述|
|--- |--- |
|1| 群集服务 PID。|
|2| 处理 volsnap 查询的线程 TID。|
|3| 此参数的值为 1，如果我们出过程中超时 CSV 卷处于活动状态并且 2 如果我们超时后关闭 CSV 卷。|
|4| 保留。|


## <a name="cause"></a>原因
-----

对查询快照信息 volsnap 的群集服务调用时间太长。

（此代码可以永远不会用于实际的执行错误检查。）

## <a name="resolution"></a>分辨率
----------
 

## <a name="see-also"></a>请参阅
----------

[故障排除挂起使用实时转储 （博客）](https://techcommunity.microsoft.com/t5/Failover-Clustering/bg-p/FailoverClustering)

[Bug 检查代码参考](bug-check-code-reference2.md)




