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
ms.openlocfilehash: a4b4eab6982c2958f3d0160ae1991bd2b94a9572
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67367644"
---
# <a name="bug-check-0x1a0-ttmwatchdogtimeout"></a>Bug 检查 0x1A0：TTM\_监视器\_超时

TTM\_监视器\_超时错误检查的值为 0x000001A0。 这表示终端拓扑管理器检测到，已配置的超时的一些设备特定操作未完成。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://support.microsoft.com/help/14238/windows-10-troubleshoot-blue-screen-errors)。

 

## <a name="ttmwatchdogtimeout-parameters"></a>TTM\_监视器\_超时参数

|参数|描述|
|--- |--- |
|1| 失败类型-下面列出的值。|
|2| 到设备的指针。 |
|3| 指向工作线程。|
|4| 标注例程的指针。 |

**失败类型**

0x1:设备分配给终端未取得进展。

0x2:设备的关闭回调未取得进展。

0x3:设备的设置输入模式回调未取得进展。

0x4:设备的设置显示状态回调未取得进展。

0x5:设置设备的内置面板状态未取得进展。

0x6:更新设备的主显示器的可见状态未取得进展。

## <a name="cause"></a>原因
-----

终端拓扑管理器检测到，已配置的超时的一些设备特定操作未完成。


## <a name="see-also"></a>请参阅
----------

[Bug 检查代码参考](bug-check-code-reference2.md)

