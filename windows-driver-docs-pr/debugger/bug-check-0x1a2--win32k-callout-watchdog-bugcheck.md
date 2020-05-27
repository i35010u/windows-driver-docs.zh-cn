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
ms.openlocfilehash: a3e7a1973b07b6171b96f8dc696c1f62d9a6248c
ms.sourcegitcommit: 2f37e8de9759164804a3b1c7f5c9e497a607539b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/26/2020
ms.locfileid: "83852122"
---
# <a name="bug-check-0x1a2-win32k_callout_watchdog_bugcheck"></a>Bug 检查0x1A2： WIN32K.SYS \_ 标注 \_ 监视器 \_ 错误检查

> [!IMPORTANT]
> 本主题适用于程序员。 如果你是在使用计算机时收到蓝屏错误代码的客户，请参阅[排查蓝屏错误](https://www.windows.com/stopcode)。

WIN32K.SYS \_ 标注 \_ 监视程序 \_ 错误检查实时转储的值为0x000001A2。 它指示 Win32k.sys 的标注不会立即返回。

## <a name="win32k_callout_watchdog_bugcheck-parameters"></a>WIN32K.SYS \_ 标注 \_ 监视器 \_ 错误检测参数

以下参数显示在蓝色屏幕上。

| 参数 |                        说明                    |
|-----------|-------------------------------------------------------|
|     1     | 线程阻塞提示从 Win32k.sys 标注返回。  |
|     2     | 保留。                                             |
|     3     | 保留。                                             |
|     4     | 保留。                                             |
