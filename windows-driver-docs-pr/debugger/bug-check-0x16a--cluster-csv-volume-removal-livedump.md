---
title: Bug 检查 0x16A CLUSTER_CSV_VOLUME_REMOVAL_LIVEDUMP
description: CLUSTER_CSV_VOLUME_REMOVAL_LIVEDUMP bug 检查具有 0x0000016A 值。 这表示群集共享卷管理器卷删除请求已超时。
keywords:
- Bug 检查 0x16A CLUSTER_CSV_VOLUME_REMOVAL_LIVEDUMP
- CLUSTER_CSV_VOLUME_REMOVAL_LIVEDUMP
ms.date: 01/03/2019
topic_type:
- apiref
api_name:
- CLUSTER_CSV_VOLUME_REMOVAL_LIVEDUMP
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f39f8917244fc2ed35e1f60a6cb9d022689e5d60
ms.sourcegitcommit: fb8b1d2e18dd727e8a479b04c9e6051e7e9fa484
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/18/2019
ms.locfileid: "59238502"
---
# <a name="bug-check-0x16a-clustercsvvolumeremovallivedump"></a>Bug 检查 0x16A：群集\_CSV\_卷\_删除\_LIVEDUMP

群集\_CSV\_卷\_删除\_LIVEDUMP bug 检查的值为 0x0000016A。 这表示群集共享卷管理器卷删除请求已超时。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。



## <a name="clustercsvvolumeremovallivedump-parameters"></a>群集\_CSV\_卷\_删除\_LIVEDUMP 参数

|参数|描述|
|--- |--- |
|1| 群集服务 PID|
|2| 保留。|
|3| 保留。|
|4| 保留。|

## <a name="cause"></a>原因
-----
群集共享卷管理器卷删除请求已超时。

系统生成的转储实时的分析的延迟。

（此代码可以永远不会用于实际的执行错误检查。）

## <a name="resolution"></a>分辨率
----------
 

## <a name="see-also"></a>请参阅
----------

[故障排除挂起使用实时转储 （博客）](https://blogs.msdn.microsoft.com/clustering/2016/03/02/troubleshooting-hangs-using-live-dump/)

[Bug 检查代码参考](bug-check-code-reference2.md)




