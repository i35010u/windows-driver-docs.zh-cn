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
ms.openlocfilehash: f616809d818829c04a460f9d9c7dc2d384ead450
ms.sourcegitcommit: fb8b1d2e18dd727e8a479b04c9e6051e7e9fa484
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/18/2019
ms.locfileid: "59238426"
---
# <a name="bug-check-0x171-clustercsvclussvcdisconnectwatchdog"></a>Bug 检查 0x171：群集\_CSV\_CLUSSVC\_断开连接\_监视器

群集\_CSV\_CLUSSVC\_断开连接\_监视器 bug 检查的值为 0x00000171。 这表示群集断开连接不使进程向前推进。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。



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




