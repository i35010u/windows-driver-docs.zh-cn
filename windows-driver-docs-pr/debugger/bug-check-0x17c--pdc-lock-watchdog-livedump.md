---
title: Bug 检查 17 C PDC_LOCK_WATCHDOG_LIVEDUMP
description: PDC_LOCK_WATCHDOG_LIVEDUMP bug 检查具有 0x0000017C 值。 这表示线程具有已持有 PDC 锁的时间太长。
keywords:
- Bug 检查 17 C PDC_LOCK_WATCHDOG_LIVEDUMP
- PDC_LOCK_WATCHDOG_LIVEDUMP
ms.date: 01/04/2019
topic_type:
- apiref
api_name:
- PDC_LOCK_WATCHDOG_LIVEDUMP
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 1630401cd7c5562c7faadc25c650b67eade9fd10
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67391975"
---
# <a name="bug-check-17c-pdclockwatchdoglivedump"></a>Bug 检查 17 C:PDC\_锁\_监视器\_LIVEDUMP

PDC\_锁\_监视器\_LIVEDUMP bug 检查的值为 0x0000017C。 这表示线程具有已持有 PDC 锁的时间太长。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://support.microsoft.com/help/14238/windows-10-troubleshoot-blue-screen-errors)。


 ## <a name="pdclockwatchdoglivedump-parameters"></a>PDC\_锁\_监视器\_LIVEDUMP 参数

|参数|描述|
|--- |--- |
|1| 持有 PDC 锁的线程。|
|2| 锁监视器超时以毫秒为单位。 |
|3| 保留。 |
|4| 保留。 |


## <a name="cause"></a>原因
-----
线程具有已持有 PDC 锁的时间太长。 Livedump 旨在提供信息来调查。 

（此代码可以永远不会用于实际的执行错误检查。）

## <a name="resolution"></a>分辨率
-----

使用调试器[！ 线程](-thread.md)命令以显示持有的锁的参数 1 中提供的线程。  分析该代码，以确定为什么它持有锁而使超出超时期限。


## <a name="see-also"></a>请参阅
----------

[Bug 检查代码参考](bug-check-code-reference2.md)

[\!thread](-thread.md)


 




