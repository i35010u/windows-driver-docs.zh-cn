---
title: Bug 检查 1A1 WIN32K_CALLOUT_WATCHDOG_LIVEDUMP
description: WIN32K_CALLOUT_WATCHDOG_LIVEDUMP 的值为0x000001A1。
keywords:
- Bug 检查 0x1A1 WIN32K_CALLOUT_WATCHDOG_LIVEDUMP
- WIN32K_CALLOUT_WATCHDOG_LIVEDUMP
ms.date: 02/12/2020
topic_type:
- apiref
api_name:
- WIN32K_CALLOUT_WATCHDOG_LIVEDUMP
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 69a3e7fbf651f7d951b21594ba476ec7a2f87a02
ms.sourcegitcommit: 2f37e8de9759164804a3b1c7f5c9e497a607539b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/26/2020
ms.locfileid: "83852124"
---
# <a name="bug-check-0x1a1-win32k_callout_watchdog_livedump"></a>Bug 检查0x1A1： WIN32K.SYS \_ 标注 \_ 监视器 \_ LIVEDUMP

> [!IMPORTANT]
> 本主题适用于程序员。 如果你是在使用计算机时收到蓝屏错误代码的客户，请参阅[排查蓝屏错误](https://www.windows.com/stopcode)。

WIN32K.SYS \_ CALLOUT \_ 看门程序 \_ LIVEDUMP 实时转储的值为0x000001A1。 Win32k.sys 的标注不会立即返回。

## <a name="win32k_callout_watchdog_livedump-parameters"></a>WIN32K.SYS \_ 标注 \_ 监视器 \_ LIVEDUMP 参数

以下参数显示在蓝色屏幕上。

| 参数 |                        说明                    |
|-----------|-------------------------------------------------------|
|     1     | 线程阻塞提示从 Win32k.sys 标注返回。  |
|     2     | 保留。                                             |
|     3     | 保留。                                             |
|     4     | 保留。                                             |

## <a name="cause"></a>原因

Win32k.sys 的标注不会立即返回。

（此代码永远不能用于实际错误检查; 它用于标识实时转储。）
