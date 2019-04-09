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
ms.openlocfilehash: 0103223a4cc14431db4a0d6aa3714063c4c49467
ms.sourcegitcommit: 55d7f63bb9e7668d65aa0999e65d18fabd44758e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2019
ms.locfileid: "59238648"
---
# <a name="bug-check-0x166-clusterresourcecalltimeoutlivedump"></a>Bug 检查 0x166：群集\_资源\_调用\_超时\_LIVEDUMP

群集\_资源\_调用\_超时\_LIVEDUMP bug 检查的值为 0x00000166。 这指示群集资源调用所花时间超过配置的超时值。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。



## <a name="clusterresourcecalltimeoutlivedump-parameters"></a>群集\_资源\_调用\_超时\_LIVEDUMP 参数

|参数|描述|
|--- |--- |
|1|资源主机监视器 PID。|
|2|处理资源调用的线程 TID。|
|3|资源调用类型-下面列出。|
|4|子代码。 当参数 3 等于 8，则此参数包含群集资源的控制代码。 当参数 3 等于 9，则此参数包含群集资源类型控制代码。|

**资源调用类型**

1 打开

关闭 2

联机 3

脱机 4

5 终止

6 进行仲裁

7 版本

8 资源控制

9 的资源类型的控件

10 查找保持活动状态

11 处于活动状态

12 故障通知

13 关闭进程

14 取消


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




