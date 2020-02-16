---
title: Bug 检查 1A2 WIN32K_CALLOUT_WATCHDOG_BUGCHECK
description: WIN32K_CALLOUT_WATCHDOG_BUGCHECK 的实时转储的值为0x000001A2。
keywords:
- Bug 检查 0x1A2 WIN32K_CALLOUT_WATCHDOG_BUGCHECK
- WIN32K_CALLOUT_WATCHDOG_BUGCHECK
ms.date: 02/12/2020
topic_type:
- apiref
api_name:
- WIN32K_CALLOUT_WATCHDOG_BUGCHECK
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 3a4a8a3e23094476f0bf3f09e34a6b8c187ef40b
ms.sourcegitcommit: f931a1bad4132c07be5966b428c77745c96bcba4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/14/2020
ms.locfileid: "77340086"
---
# <a name="bug-check-bug-check-0x1a2-win32k_callout_watchdog_bugcheck"></a>Bug 检查 Bug 检查0x1A2： WIN32K.SYS\_CALLOUT\_监视器\_检测错误

> [!IMPORTANT]
> 本主题面向程序员。 如果你是在使用计算机时收到蓝屏错误代码的客户，请参阅[排查蓝屏错误](https://www.windows.com/stopcode)。

WIN32K.SYS\_标注\_监视器\_错误检查实时转储的值为0x000001A2。 它指示 Win32k.sys 的标注不会立即返回。

## <a name="win32k_callout_watchdog_bugcheck-parameters"></a>WIN32K.SYS\_标注\_监视器\_检测错误参数

以下参数显示在蓝色屏幕上。

| 参数 |                        说明                    |
|-----------|-------------------------------------------------------|
|     1     | 线程阻塞提示从 Win32k.sys 标注返回。  |
|     2     | 保留。                                             |
|     3     | 保留。                                             |
|     4     | 保留。                                             |
