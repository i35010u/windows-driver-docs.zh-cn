---
title: Bug 检查 0x1CA SYNTHETIC_WATCHDOG_TIMEOUT
description: SYNTHETIC_WATCHDOG_TIMEOUT bug 检查的值为0x000001CA。 系统范围的监视程序已过期。 这表示系统挂起，未处理计时器时钟周期。
keywords:
- Bug 检查 0x1CA SYNTHETIC_WATCHDOG_TIMEOUT
- SYNTHETIC_WATCHDOG_TIMEOUT
ms.date: 01/29/2021
topic_type:
- apiref
api_name:
- SYNTHETIC_WATCHDOG_TIMEOUT
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 508a6e565a5aa2218e7f8281e30964134388fdaf
ms.sourcegitcommit: 597ef5dc63565202a8c6d9e51c9faf1b6398968a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/29/2021
ms.locfileid: "99081119"
---
# <a name="bug-check-0x1ca-synthetic_watchdog_timeout"></a>Bug 检查0x1CA：综合 \_ 监视器 \_ 超时

综合 \_ 监视器 \_ 超时 bug 检查的值为0x000001CA。 系统范围的监视程序已过期。 这表示系统挂起，未处理计时器时钟周期。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。

## <a name="synthetic_watchdog_timeout-parameters"></a>综合 \_ 监视程序 \_ 超时参数

|参数|说明|
|-------- |---------- |
|1|上次重置监视程序的时间，以中断时间为间隔。|
|2| 当前中断时间。 |
|3| 当前的 QPC 时间戳。 |
|4| 时钟处理器的索引。 |

## <a name="cause"></a>原因

系统范围的监视程序已过期。 这表示系统挂起，未处理计时器时钟周期。

## <a name="resolution"></a>解决方法

[**！分析**](-analyze.md)调试器扩展显示有关 bug 检查的信息，可帮助确定根本原因。 有关 WinDbg 和 **！分析** 的详细信息，请参阅 [使用！分析扩展](using-the--analyze-extension.md) 和 [！分析](-analyze.md)。


## <a name="see-also"></a>另请参阅

[Bug 检查代码参考](bug-check-code-reference2.md)
