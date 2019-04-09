---
title: Bug 检查 0x16B CLUSTER_CSV_CLUSTER_WATCHDOG_LIVEDUMP
description: CLUSTER_CSV_CLUSTER_WATCHDOG_LIVEDUMP bug 检查具有 0x0000016B 值。 这表示群集服务用户模式下监视程序检测到，一个线程长时间未发出向前推进。
keywords:
- Bug 检查 0x16B CLUSTER_CSV_CLUSTER_WATCHDOG_LIVEDUMP
- CLUSTER_CSV_CLUSTER_WATCHDOG_LIVEDUMP
ms.date: 01/03/2019
topic_type:
- apiref
api_name:
- CLUSTER_CSV_CLUSTER_WATCHDOG_LIVEDUMP
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 80a06858183ca571bc5fafe2bf3802855a3a2ad1
ms.sourcegitcommit: 55d7f63bb9e7668d65aa0999e65d18fabd44758e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2019
ms.locfileid: "59238480"
---
# <a name="bug-check-0x16b-clustercsvclusterwatchdoglivedump"></a>Bug 检查 0x16B：群集\_CSV\_群集\_监视器\_LIVEDUMP

群集\_CSV\_群集\_监视器\_LIVEDUMP bug 检查的值为 0x0000016B。 这表示群集服务用户模式下监视程序检测到，一个线程长时间未发出向前推进。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。



## <a name="clustercsvclusterwatchdoglivedump-parameters"></a>群集\_CSV\_群集\_监视器\_LIVEDUMP 参数

|参数|描述|
|--- |--- |
|1| 群集服务 PID。|
|2| 处于停滞状态的线程 id。|
|3| 保留。|
|4| 保留。|

## <a name="cause"></a>原因
-----

群集服务用户模式下监视程序检测到，一个线程长时间未发出向前推进。

系统生成的转储实时的分析的延迟。

（此代码可以永远不会用于实际的执行错误检查。）

## <a name="resolution"></a>分辨率
----------
 

## <a name="see-also"></a>请参阅
----------

[故障排除挂起使用实时转储 （博客）](https://blogs.msdn.microsoft.com/clustering/2016/03/02/troubleshooting-hangs-using-live-dump/)

[Bug 检查代码参考](bug-check-code-reference2.md)




