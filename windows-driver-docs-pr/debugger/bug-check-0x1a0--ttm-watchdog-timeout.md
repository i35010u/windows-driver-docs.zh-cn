---
title: Bug 检查 0x1A0 TTM_WATCHDOG_TIMEOUT
description: TTM_WATCHDOG_TIMEOUT bug 检查具有 0x000001A0 值。 这表示终端拓扑管理器检测到，已配置的超时的一些设备特定操作未完成。
keywords:
- Bug 检查 0x1A0 TTM_WATCHDOG_TIMEOUT
- TTM_WATCHDOG_TIMEOUT
ms.date: 01/04/2019
topic_type:
- apiref
api_name:
- TTM_WATCHDOG_TIMEOUT
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: afe9cab920ff14f4c37b61eb4a2f75b2f39d4853
ms.sourcegitcommit: ece0a2affa08f1b6446368ede06040b3153aaae2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/23/2019
ms.locfileid: "56743514"
---
# <a name="bug-check-0x1a0-ttmwatchdogtimeout"></a>Bug 检查 0x1A0:TTM\_监视器\_超时

TTM\_监视器\_超时错误检查的值为 0x000001A0。 这表示终端拓扑管理器检测到，已配置的超时的一些设备特定操作未完成。

**重要**本主题适用于程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。
 

## <a name="ttmwatchdogtimeout-parameters"></a>TTM\_监视器\_超时参数

|参数|描述|
|--- |--- |
|1| 失败类型-下面列出的值。|
|2| 到设备的指针。 |
|3| 指向工作线程。|
|4| 标注例程的指针。 |

**失败类型**

     0x1 : A device assignment to a terminal is not making progress.
     0x2 : Device's close callback is not making progress.
     0x3 : Device's set-input-mode callback is not making progress.
     0x4 : Device's set-display-state callback is not making progress.
     0x5 : Setting device's built-in panel state is not making progress.
     0x6 : Updating device's primary display visible state is not making progress.

## <a name="cause"></a>原因
-----

终端拓扑管理器检测到，已配置的超时的一些设备特定操作未完成。


## <a name="see-also"></a>请参阅
----------

[Bug 检查代码参考](bug-check-code-reference2.md)

