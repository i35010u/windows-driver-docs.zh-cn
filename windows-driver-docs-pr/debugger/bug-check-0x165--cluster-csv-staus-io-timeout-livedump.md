---
title: Bug 检查 0x165 CLUSTER_CSV_STATUS_IO_TIMEOUT_LIVEDUMP
description: CLUSTER_CSV_STATUS_IO_TIMEOUT_LIVEDUMP bug 检查具有 0x00000165 值。 这表明 SMB 客户端遇到了超时情况。
keywords:
- Bug 检查 0x165 CLUSTER_CSV_STATUS_IO_TIMEOUT_LIVEDUMP
- CLUSTER_CSV_STATUS_IO_TIMEOUT_LIVEDUMP
ms.date: 01/03/2019
topic_type:
- apiref
api_name:
- CLUSTER_CSV_STATUS_IO_TIMEOUT_LIVEDUMP
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ea0567ae1faa6321fdec5f3e72e5d7771a61223f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63342543"
---
# <a name="bug-check-0x165-clustercsvstatusiotimeoutlivedump"></a>Bug 检查 0x165：群集\_CSV\_状态\_IO\_超时\_LIVEDUMP

群集\_CSV\_状态\_IO\_超时\_LIVEDUMP bug 检查的值为 0x00000165。 这表示非协调节点上的 SMB 客户端协调的节点上的 IO 时间太长并且失败的 STATUS_IO_TIMEOUT 所有 Io 错误报告。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。


## <a name="clustercsvstatusiotimeoutlivedump-parameters"></a>群集\_CSV\_状态\_IO\_超时\_LIVEDUMP 参数

|参数|描述|
|--- |--- |
|1|可选的群集服务 PID。|
|2|观察到 STATUS_IO_TIMEOUT 的节点的群集节点 Id。|
|3|保留。|
|4|保留。|

## <a name="cause"></a>原因
-----

协调的节点上的 IO 时间太长并且失败的 STATUS_IO_TIMEOUT 所有 Io，会显示错误的非协调节点上的 SMB 客户端。

在转储的辅助数据的流提供了其他信息。

（此代码可以永远不会用于实际的执行错误检查; 它用于标识包括群集共享卷遥测数据的实时转储）。


## <a name="resolution"></a>分辨率
----------
 

## <a name="see-also"></a>请参阅
----------

[故障排除挂起使用实时转储 （博客）](https://blogs.msdn.microsoft.com/clustering/2016/03/02/troubleshooting-hangs-using-live-dump/)

[Bug 检查代码参考](bug-check-code-reference2.md)




