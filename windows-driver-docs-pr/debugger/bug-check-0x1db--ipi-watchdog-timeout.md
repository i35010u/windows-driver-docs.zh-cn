---
title: Bug 检查 0x1DB IPI_WATCHDOG_TIMEOUT
description: IPI_WATCHDOG_TIMEOUT bug 检查具有 0x000001DB 值。 它指示的一个处理器已超过允许的时间卡在 IPI 循环。
keywords:
- Bug 检查 0x1DB IPI_WATCHDOG_TIMEOUT
- IPI_WATCHDOG_TIMEOUT
ms.date: 01/14/2019
topic_type:
- apiref
api_name:
- IPI_WATCHDOG_TIMEOUT
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b570272f29bf2878e4dde15d28da6e64f2c1ae27
ms.sourcegitcommit: ece0a2affa08f1b6446368ede06040b3153aaae2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/23/2019
ms.locfileid: "56743476"
---
# <a name="bug-check-0x1db-ipiwatchdogtimeout"></a>Bug 检查 0x1DB:IPI\_监视器\_超时

IPI\_监视器\_超时错误检查的值为 0x000001DB。 它指示，一个处理器具有 IPI 循环中停滞超过允许的时间。

**重要**本主题适用于程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。
 

## <a name="ipiwatchdogtimeout-parameters"></a>IPI\_监视器\_超时参数

|参数|描述|
|-------- |---------- |
|1| 指示 QPC 频率。  |
|2| 指示当前 QPC。 |
|3| 指示基线 QPC。 |
|4| 保留。 |


## <a name="cause"></a>原因
-----

允许的时间超过已将一个处理器卡在 IPI 循环。


## <a name="see-also"></a>请参阅
----------

[Bug 检查代码参考](bug-check-code-reference2.md)

