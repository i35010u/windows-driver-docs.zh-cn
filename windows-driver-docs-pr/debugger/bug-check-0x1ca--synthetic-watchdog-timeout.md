---
title: Bug 检查 0x1CA SYNTHETIC_WATCHDOG_TIMEOUT
description: SYNTHETIC_WATCHDOG_TIMEOUT bug 检查具有 0x000001CA 值。 系统宽监视器已过期。 这表明系统已挂起和未处理计时器时钟周期。
keywords:
- Bug 检查 0x1CA SYNTHETIC_WATCHDOG_TIMEOUT
- SYNTHETIC_WATCHDOG_TIMEOUT
ms.date: 01/11/2019
topic_type:
- apiref
api_name:
- SYNTHETIC_WATCHDOG_TIMEOUT
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b8ed289e8e8b2e1d7264d8a9d33813d6151a090c
ms.sourcegitcommit: 55d7f63bb9e7668d65aa0999e65d18fabd44758e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2019
ms.locfileid: "59239806"
---
# <a name="bug-check-0x1ca-syntheticwatchdogtimeout"></a>Bug 检查 0x1CA：综合\_监视器\_超时

合成\_监视器\_超时错误检查的值为 0x000001CA。 系统宽监视器已过期。 这表明系统已挂起和未处理计时器时钟周期。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。

 

## <a name="syntheticwatchdogtimeout-parameters"></a>综合\_监视器\_超时参数

|参数|描述|
|-------- |---------- |
|1|自监视器上次重置，在中断时间以来的时间。|
|2| 当前的中断时间。 |
|3| 当前 QPC 时间戳。 |
|4| 时钟处理器的索引。 |

## <a name="cause"></a>原因
-----

系统宽监视器已过期。 这表明系统已挂起和未处理计时器时钟周期。


## <a name="see-also"></a>请参阅
----------

[Bug 检查代码参考](bug-check-code-reference2.md)

