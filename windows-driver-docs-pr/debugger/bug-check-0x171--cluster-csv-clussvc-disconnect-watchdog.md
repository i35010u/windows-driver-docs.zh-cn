---
title: Bug 检查 0x171 CLUSTER_CSV_CLUSSVC_DISCONNECT_WATCHDOG
description: CLUSTER_CSV_CLUSSVC_DISCONNECT_WATCHDOG bug 检查具有 0x00000171 值。 这表示群集断开连接不使进程向前推进。
keywords:
- Bug 检查 0x171 CLUSTER_CSV_CLUSSVC_DISCONNECT_WATCHDOG
- CLUSTER_CSV_CLUSSVC_DISCONNECT_WATCHDOG
ms.date: 01/03/2019
topic_type:
- apiref
api_name:
- CLUSTER_CSV_CLUSSVC_DISCONNECT_WATCHDOG
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 3657014a3b51e5be00b196ddfd6285d221d9a1fe
ms.sourcegitcommit: ece0a2affa08f1b6446368ede06040b3153aaae2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/23/2019
ms.locfileid: "56743585"
---
# <a name="bug-check-0x171-clustercsvclussvcdisconnectwatchdog"></a>Bug 检查 0x171:群集\_CSV\_CLUSSVC\_断开连接\_监视器

群集\_CSV\_CLUSSVC\_断开连接\_监视器 bug 检查的值为 0x00000171。 这表示群集断开连接不使进程向前推进。

**重要**本主题适用于程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。


## <a name="clustercsvclussvcdisconnectwatchdog-parameters"></a>群集\_CSV\_CLUSSVC\_断开连接\_监视程序参数

|参数|描述|
|--- |--- |
|1| 处理群集断开连接的线程 id。|
|2| 以毫秒为单位的超时值。 |
|3| 保留 |
|4| 保留 |

## <a name="cause"></a>原因
-----

群集断开连接不使进程向前推进。


## <a name="resolution"></a>分辨率
----------
 

## <a name="see-also"></a>请参阅
----------

[故障排除挂起使用实时转储 （博客）](https://blogs.msdn.microsoft.com/clustering/2016/03/02/troubleshooting-hangs-using-live-dump/)

[Bug 检查代码参考](bug-check-code-reference2.md)




